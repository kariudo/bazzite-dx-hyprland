# bazzite-dx-hyprland

A custom image based on Bazzite with the intention to keep as close to Bazzite-dx as possible but with [hyprland](https://hypr.land/) as the window manager and several pre-installed programs for enabling the expected desktop environment experience.

## General notes

Removes the following packages from `bazzite-dx-gnome`:
The build script removes the default GNOME and KDE desktop components so the image can be based around Hyprland instead.

Typical removals performed by `build_files/build.sh`:

- gnome-shell
- gnome-\*
- gdm
- plasma-workspace
- plasma-\*
- kde-\*

## Added packages

The build installs Hyprland and several utilities to provide a functional desktop experience. The main packages added by `build_files/build.sh` are:

- hyprland
- hyprpaper
- hyprpicker
- hypridle
- hyprlock
- hyprsunset
- hyprpolkitagent
- hyprsysteminfo
- hyprpanel
- hyprland-qt-support
- hyprland-qtutils
- hyprpanel.service (systemd unit enabled)
- qt6ct-kde
- alacritty
- sddm
- pipewire
- wofi
- brightnessctl

## Notes on installation

The image build script (`build_files/build.sh`):

- Removes GNOME and KDE packages using `dnf5 -y remove`.
- Temporarily enables the COPR repository `solopasha/hyprland` to install Hyprland packages, then disables it.
- Enables `podman.socket` and globally enables the `hyprpanel.service` systemd unit.

## Build & Switch

The build following the template is handled by the github action in the repo.

If you fork this repo you will need to generate a new cosign key (see Bazzite template instructions if needed), then store the .key to the repo secrets as well so the action has access.

Once built, you can switch to the image using `bootc`:

```sh
sudo bootc switch ghcr.io/kariudo/bazzite-dx-hyperland
```

## Customizing packages

If you want to customize the package list, edit `build_files/build.sh` and the `disk_config` files before running the build.
