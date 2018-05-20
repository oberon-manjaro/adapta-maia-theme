# Maintainer: Stefano Capitani <stefano_at_manjaro_dot_org>
# Maintainer: Bernhard Landauer <oberon@manjaro.org>
# Contributor: ceyhunnabiyev for Breath color and Adapta Black variation <https://github.com/ceyhunnabiyev>

pkgname=adapta-maia-theme
_pkgname=adapta-gtk-theme
pkgver=3.93.1.16
pkgrel=1
pkgdesc="An adaptive Gtk+ theme based on Material Design Guidelines.Build with Manjaro Maia color"
arch=(any)
url="https://github.com/adapta-project/${_pkgname}"
license=('GPL2' 'CCPL')
optdepends=('ttf-roboto: The recommended font'
            'noto-fonts: The recommended font for improved language support'
            'gtk-engine-murrine: for gtk2 themes'
            'kvantum-manjaro: qt5 engine for adapta')
makedepends=('libxml2'
             'libsass'
             'sassc'
             'librsvg'
             'inkscape'
             'libcanberra'
             'parallel')
validpgpkeys=('2C675EC71CF31D4652AB608616A443152D7A865E')	     
source=("${_pkgname}-${pkgver}.tar.gz::${url}/archive/${pkgver}.tar.gz"
        "${url}/releases/download/${pkgver}/${_pkgname}-${pkgver}.tar.gz.asc"
        'XfdesktopIconView.patch')
sha256sums=('b8608829471018584ed5b6a66c8abe4a4fa5994d87bff8769f94da539c94e705'
            'SKIP'
            'a7b7d3ac846a671a683d7cf8036b3cd81f7e2896d0ab506db3dc2f03b83e3223')
            
prepare() {
    cd $_pkgname-$pkgver
    patch -p1 -i $srcdir/XfdesktopIconView.patch
}

build() {
    cd $_pkgname-$pkgver

    find . -type f -name '*.*' -exec sed -i \
      "s/#00BCD4/#16a085/Ig" {} \;

    find ./extra/gedit/adapta.xml \
      ./extra/plank/dock.theme \
      ./extra/telegram/dark/colors.tdesktop-theme \
      ./extra/telegram/light/colors.tdesktop-theme \
      ./gtk/asset/assets-gtk2.svg.in \
      ./gtk/asset/assets-gtk3.svg.in \
      ./gtk/asset/assets-clone/z-depth-1.svg \
      ./gtk/asset/assets-clone/z-depth-2.svg \
      ./gtk/gtk-2.0/colors.rc.in \
      ./gtk/gtk-2.0/colors-dark.rc.in \
      ./gtk/gtk-2.0/common.rc \
      ./gtk/gtk-2.0/common-eta.rc \
      ./gtk/sass/common/_colors.scss \
      ./m4/adapta-color-scheme.m4 \
      ./shell/asset/assets-cinnamon/ \
      ./shell/asset/assets-gnome-shell/ \
      ./shell/asset/assets-xfce/ \
      ./shell/sass/common/_colors.scss \
      ./shell/sass/gnome-shell/3.24/_extension-workspaces-to-dock.scss \
      ./shell/sass/gnome-shell/3.26/_extension-workspaces-to-dock.scss \
      ./shell/xfce-notify-4.0/gtkrc \
      ./wm/asset/assets-metacity/ \
      ./wm/asset/assets-openbox/ \
      ./wm/asset/assets-xfwm/ \
      ./wm/metacity-1/metacity-theme-2.xml \
      ./wm/openbox-3/themerc \
      ./wm/openbox-3/themerc-nokto \
      ./wm/xfwm4/themerc -type f -print | xargs sed -i -e \
      's/#2196F3/#38a8a3/Ig'  -e \
      's/#03A9f4/#299984/Ig'

    ./autogen.sh --prefix "${pkgdir}/usr" \
      --enable-plank \
      --enable-telegram \
      --enable-parallel
    make
}

package() {
    cd $_pkgname-$pkgver
    make install
    install -dm 755 $pkgdir/usr/share/plank/themes
    ln -s /usr/share/themes/Adapta-Maia/plank $pkgdir/usr/share/plank/themes/Adapta-Maia

    install -Dm 644 LICENSE_CC_BY_SA4 -t $pkgdir/usr/share/licenses/adapta-maia-theme/

    # rename folders
    cd "$pkgdir/usr/share/themes"
    mv Adapta Adapta-Maia
    mv Adapta-Nokto Adapta-Nokto-Maia
    mv Adapta-Eta Adapta-Eta-Maia
    mv Adapta-Nokto-Eta Adapta-Nokto-Eta-Maia

    # Modify index.theme
    sed -i -e 's,.*Adapta.*,Adapta-Maia,' $pkgdir/usr/share/themes/Adapta-Maia/index.theme
    sed -i -e 's,.*Adapta-Nokto.*,Adapta-Nokto-Maia,' $pkgdir/usr/share/themes/Adapta-Nokto-Maia/index.theme
    sed -i -e 's,.*Adapta-Eta.*,Adapta-Eta-Maia,' $pkgdir/usr/share/themes/Adapta-Eta-Maia/index.theme
    sed -i -e 's,.*Adapta-Nokto-Eta.*,Adapta-Nokto-Eta-Maia,' $pkgdir/usr/share/themes/Adapta-Nokto-Eta-Maia/index.theme

    # symlink
    cd "$pkgdir/usr/share/themes/Adapta-Nokto-Maia"
    ln -sf /usr/share/themes/Adapta-Maia/xfwm4 xfwm4
    ln -sf /usr/share/themes/Adapta-Maia/xfce-notify-4.0 xfce-notify-4.0
    ln -sf /usr/share/themes/Adapta-Maia/plank plank
    ln -sf /usr/share/themes/Adapta-Maia/gedit gedit
    ln -sf /usr/share/themes/Adapta-Maia/metacity-1 metacity-1
    ln -sf /usr/share/themes/Adapta-Maia/gtk-3.22 gtk-3.22
    ln -sf /usr/share/themes/Adapta-Maia/gtk-3.0 gtk-3.0

    cd "$pkgdir/usr/share/themes/Adapta-Eta-Maia"
    ln -sf /usr/share/themes/Adapta-Maia/xfce-notify-4.0 xfce-notify-4.0
    ln -sf /usr/share/themes/Adapta-Maia/plank plank
    ln -sf /usr/share/themes/Adapta-Maia/telegram telegram
    ln -sf /usr/share/themes/Adapta-Maia/metacity-1 metacity-1

    cd "$pkgdir/usr/share/themes/Adapta-Nokto-Eta-Maia"
    ln -sf /usr/share/themes/Adapta-Eta-Maia/gtk-3.22 gtk-3.22
    ln -sf /usr/share/themes/Adapta-Maia/metacity-1 metacity-1
    ln -sf /usr/share/themes/Adapta-Maia/plank plank
    ln -sf /usr/share/themes/Adapta-Nokto-Maia/telegram telegram
    ln -sf /usr/share/themes/Adapta-Maia/xfce-notify-4.0 xfce-notify-4.0
}
