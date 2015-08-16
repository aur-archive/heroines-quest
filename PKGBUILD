# Maintainer: Ner0
# The launch script is based on Tea23's scripts (https://github.com/Tea23/arch-gog)

pkgname=heroines-quest
pkgver=1.1
pkgrel=1
pkgdesc="Heroine's Quest: Herald of Ragnarok, a Quest for Glory-inspired adventure/RPG"
arch=('any')
url="http://crystalshard.net/hq.htm"
license=('custom')
depends=('ags-git' 'unionfs-fuse')
options=('!strip')
install=heroines-quest.install
noextract=("$pkgname-$pkgver.zip")
source=("$pkgname.desktop"
	"$pkgname.png"
	"$pkgname.sh")
md5sums=('483f0fdbeb81503785bfc17af55f954b'
         '98e86babe89ca7af075cfef9dc7d8053'
         'c37a2bad8338bd0e5239ca82bbb3c3c9'
         '066f68e1a284ca673068d2036984455f')
# http://mirror.nostalgicgamer.co.uk/games/HeroinesQuest.zip
_mirror=$(curl -s http://www.moddb.com/downloads/start/63540/all | grep -o \
"/downloads/mirror/[0-9].*/[0-9].*/" | head -n 1 | sed 's/\" id=.*//')
source+=($pkgname-$pkgver.zip::http://www.moddb.com$_mirror)

PKGEXT='.pkg.tar'

package() {
  # Creating the dirs
  install -dm755 "$pkgdir/opt/ags/$pkgname"

  # Extracting the game
  bsdtar -xf $pkgname-$pkgver.zip -C "$pkgdir/opt/ags/$pkgname"

  # Editing the configuration file
  sed -i 's/windowed=1/windowed=0/' "$pkgdir/opt/ags/$pkgname/acsetup.cfg"
  sed -i 's/gfxfilter=max/gfxfilter=StdScale2\nantialias=1/' "$pkgdir/opt/ags/$pkgname/acsetup.cfg"

  # Installing the manual
  install -Dm644 "$pkgdir/opt/ags/$pkgname/Heroine's Quest manual.pdf" "$pkgdir/usr/share/doc/$pkgname/Manual.pdf"

  # Removing unnecessary files
  rm -f "$pkgdir"/opt/ags/$pkgname/{*.png,*.lnk,*.jpg,*.txt,*.pdf}

  # Installing the launch script and the desktop file
  install -Dm755 "$srcdir/$pkgname.sh" "$pkgdir/usr/bin/$pkgname"
  install -Dm644 "$srcdir/$pkgname.png" "$pkgdir/usr/share/pixmaps/$pkgname.png"
  install -Dm644 "$srcdir/$pkgname.desktop" "$pkgdir/usr/share/applications/$pkgname.desktop"
}
