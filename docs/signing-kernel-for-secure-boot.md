# Signing a Linux Kernel for Secure Boot

Referenced [Surface Linux Key Signing](https://github.com/jakeday/linux-surface/blob/master/SIGNING.md)

Instructions are for ubuntu, but should work similar for other distros, if they are using shim
and grub as bootloader. If your distro is not using shim (e.g. Linux Foundation Preloader), there
should be similar steps to complete the signing (e.g. HashTool instead of MokUtil for LF Preloader)
or you can install shim to use instead. The ubuntu package for shim is called `shim-signed`, but
please inform yourself on how to install it correctly, so you do not mess up your bootloader.

Since the most recent GRUB2 update (2.02+dfsg1-5ubuntu1) in Ubuntu, GRUB2 does not load unsigned
kernels anymore, as long as Secure Boot is enabled. Users of Ubuntu 18.04 will be notified during
upgrade of the grub-efi package, that this kernel is not signed and the upgrade will abort.

Instructions adapted from [the Ubuntu Blog](https://blog.ubuntu.com/2017/08/11/how-to-sign-things-for-secure-boot).
Before following, please backup your /boot/EFI directory, so you can restore everything. Follow
these steps on your own risk.

## Create Signing Keys

1. Create the config to create the signing key, save as mokconfig.cnf:

    ```bash
    # This definition stops the following lines failing if HOME isn't
    # defined.
    HOME                    = .
    RANDFILE                = $ENV::HOME/.rnd 
    [ req ]
    distinguished_name      = req_distinguished_name
    x509_extensions         = v3
    string_mask             = utf8only
    prompt                  = no

    [ req_distinguished_name ]
    countryName             = <YOURcountrycode>
    stateOrProvinceName     = <YOURstate>
    localityName            = <YOURcity>
    0.organizationName      = <YOURorganization>
    commonName              = Secure Boot Signing Key
    emailAddress            = <YOURemail>

    [ v3 ]
    subjectKeyIdentifier    = hash
    authorityKeyIdentifier  = keyid:always,issuer
    basicConstraints        = critical,CA:FALSE
    extendedKeyUsage        = codeSigning,1.3.6.1.4.1.311.10.3.6
    nsComment               = "OpenSSL Generated Certificate"
    ```

    Adjust all parts with <YOUR*> to your details.

2. Create the public and private key for signing the kernel:

    ```bash
    openssl req -config ./mokconfig.cnf \
            -new -x509 -newkey rsa:2048 \
            -nodes -days 36500 -outform DER \
            -keyout "MOK.priv" \
            -out "MOK.der"
    ```

3. Convert the key also to PEM format (mokutil needs DER, sbsign needs PEM):

    ```bash
    openssl x509 -in MOK.der -inform DER -outform PEM -out MOK.pem
    ```

## Enroll MOK Key

1. Enroll the key to your shim installation:

    ```bash
    sudo mokutil --import MOK.der
    ```

    You will be asked for a password, you will just use it to confirm your key selection in the
    next step, so choose any.

2. Restart your system. You will encounter a blue screen of a tool called MOKManager.

    Select "Enroll MOK" and then "View key". Make sure it is your key you created in step 2.
    Afterwards continue the process and you must enter the password which you provided in
    step 4. Continue with booting your system.

3. Verify your key is enrolled via:

    ```bash
    sudo mokutil --list-enrolled
    ```

## Sign your Kernel

1. Sign your installed kernel (it should be at /boot/vmlinuz-[KERNEL-VERSION]-surface-linux-surface):

    ```bash
    sudo sbsign --key MOK.priv --cert MOK.pem /boot/vmlinuz-[KERNEL-VERSION]-generic --output /boot/vmlinuz-[KERNEL-VERSION]-generic.signed
    ```

2. Copy the initram of the unsigned kernel, so we also have an initram for the signed one.

    ```bash
    sudo cp /boot/initrd.img-[KERNEL-VERSION]-generic{,.signed}
    ```

## Update GRUB

1. Update your grub-config

    ```bash
    sudo update-grub
    ```

## Reboot and Test

1. Reboot your system and select the signed kernel. If booting works, you can remove the unsigned kernel:

    ```bash
    sudo mv /boot/vmlinuz-[KERNEL-VERSION]-generic{.signed,}
    sudo mv /boot/initrd.img-[KERNEL-VERSION]-generic{.signed,}
    sudo update-grub
    ```

Now your system should run under a signed kernel and upgrading GRUB2 works again. If you want
to upgrade the custom kernel, you can sign the new version easily by following above steps
again from step seven on. Thus BACKUP the MOK-keys (MOK.der, MOK.pem, MOK.priv).