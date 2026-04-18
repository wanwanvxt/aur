# Maintainer: Truong Vu <wanwan.vxt@gmail.com>

_pkgname=nirimod
pkgname=nirimod-git
pkgver=r22.ed97a06
pkgrel=3
pkgdesc='A visual, interactive configuration interface for the niri Wayland compositor'
arch=('any')
url='https://github.com/srinivasr/nirimod'
license=('MIT')

depends=(
    'python'
    'gtk4'
    'libadwaita'
    'python-gobject'
    'glib2'
    'pango'
    'sh'
    'niri'
)
makedepends=(
    'git'
    'python-build'
    'python-installer'
    'python-hatchling'
    'python-wheel'
)

provides=('nirimod')
conflicts=('nirimod')

source=(
    "$_pkgname::git+https://github.com/srinivasr/nirimod.git"
    "_LICENSE"
)
sha256sums=(
    'SKIP'
    'c28c2f179d5325a7fb9d58e5af0cb859c9ad895dcc5c145b16e32947d180921e'
)

pkgver() {
    cd "$srcdir/$_pkgname"
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
    cd "$srcdir/$_pkgname"
    python -m build --wheel --no-isolation
}

package() {
    cd "$srcdir/$_pkgname"

    python -m installer --destdir="$pkgdir" dist/*.whl
    install -Dm755 /dev/stdin "$pkgdir/usr/bin/nirimod" <<EOF
#!/bin/sh
exec python -m nirimod "\$@"
EOF
    install -Dm644 /dev/stdin "$pkgdir/usr/share/applications/io.github.nirimod.desktop" <<EOF
[Desktop Entry]
Version=1.0
Name=NiriMod
GenericName=Compositor Settings
Comment=GUI Configuration Manager for the Niri Wayland Compositor
Exec=nirimod
Icon=preferences-system
Terminal=false
Type=Application
Categories=Utility;Settings;DesktopSettings;
Keywords=compositor;windowmanager;wayland;niri;settings;config;
StartupNotify=true
StartupWMClass=nirimod
EOF
    install -Dm644 "$srcdir/_LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
