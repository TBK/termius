# Maintainer: TBK <aur at jjtc dot eu>
# Contributor: TBK <aur at jjtc dot eu>

pkgname=termius
pkgver=7.3.2
pkgrel=1
pkgdesc="Desktop SSH Client"
url="https://www.termius.com/"
arch=('x86_64')
license=('custom')
depends=('libnotify' 'libappindicator-gtk3' 'libxtst' 'nss' 'libxss')
makedepends=('squashfs-tools')
# Get latest version + link from https://snapcraft.io/termius-app || snap info termius-app || run the following
# curl -H 'X-Ubuntu-Series: 16' https://api.snapcraft.io/api/v1/snaps/details/termius-app | jq '.download_url' -r
# curl -H 'X-Ubuntu-Series: 16' https://api.snapcraft.io/api/v1/snaps/details/termius-app | jq '.version' -r
source=(
    "$pkgname-$pkgver.snap::https://api.snapcraft.io/api/v1/snaps/download/WkTBXwoX81rBe3s3OTt3EiiLKBx2QhuS_61.snap"
    "termius.desktop"
    "tos.html"
)
sha512sums=('430c1416f1da2e4d6fa8dab29f1cfa133cbe29eac77ad4a70a854f608e407a7715c361bd7af641b448a2c4385076181af90271b60a172f959b317cce8c5a2e89'
            '9b0788a02b9bf371de07adec8f3e14f4db8bf83dae6dee60d91027d8ba09cbab253b8b714f980d5c62b72d97e4ac11e6c3985139322bdceaad9f2f0232427656'
            '53f9c61fba12b72817c5e7f4e0ac520489265fbf425fa46f13129da66632b41a2a128072d9e0e64e37e4e8feb8424bc1c15eed127d630314e6459ceb2dbafb4b')

prepare() {
    mkdir $pkgname
    unsquashfs -f -d $pkgname $pkgname-$pkgver.snap
}

package() {
    # Option 1 - copy only the needed files ~183 MiB
    mkdir -p "$pkgdir"/opt/$pkgname

    cd "$srcdir"/$pkgname

    cp -r \
        icudtl.dat \
        libffmpeg.so \
        locales \
        resources \
        resources.pak \
        termius-app \
        v8_context_snapshot.bin \
        "$pkgdir"/opt/$pkgname
    
    cd "$srcdir"
    # Option 2 - copy all files from the .snap file ~503 MiB
    #mkdir -p "$pkgdir"/opt/
    #cp -r "$srcdir"/$pkgname "$pkgdir"/opt/$pkgname

    find "$pkgdir"/opt/$pkgname/ -type f -exec chmod 644 {} \;
    chmod 755 "$pkgdir"/opt/$pkgname/termius-app

    mkdir -p "$pkgdir"/usr/bin
    ln -sf /opt/$pkgname/termius-app "$pkgdir"/usr/bin/$pkgname
    install -Dm0644 tos.html "$pkgdir"/usr/share/licenses/$pkgname/tos.html
    install -Dm0644 $pkgname.desktop "$pkgdir"/usr/share/applications/$pkgname.desktop
    install -Dm0644 $pkgname/meta/gui/icon.png "$pkgdir"/usr/share/pixmaps/$pkgname.png
}
