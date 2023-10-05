# Why
You may want to have a back-up on your main machine for when your designated second device is not available for 2FA.
Or you might just consider 2FA annoying and superfluous for some of your accounts under your well-considered theat model.

# How

* Create directory `$HOME/.2fa`.
* Create a file in `$HOME/.2fa` that is arbitarily named indicating the account, eg `username@github` (this filename will be what rofi shows you) and put the 32-base encoded secret for the account in it. Repeat as necessary.
* Place 2fa-rofi.sh from this repo somewhere, say `~/.local/bin` and `chmod a+x ~/.local/bin/2fa-rofi.sh`
* Edit your rofi config to invoke the custom script, for example thusly `modi: "run,drun,window,ssh,2fa:/home/yourusername/.local/bin/2fa-rofi.sh";` (sadly rofi doesn't appear to expand `~` or `$HOME` when invoking custom scripts.

Bring up rofi, switch to the 2fa mode, select the account. The TOTP code will be placed in your X11 clipboard selection (edit the script if you need it to go to primary or secondary) from where you'll be able to paste it wherever it needs to go. You will also see a notification with the code (or an error, if one occurs).

# Requirements
  * rofi
  * oathtool (oath-toolkit)
  * notify-send (libnotify - if you want to see notifications)
  * xclip

# Nota bene

Obviously don't do this with your bank accounts. Secrets are stored in plaintext. Or put `~/.2fa` on an encrypted volume.
