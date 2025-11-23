
pkgname=antisos-finetuner
pkgver=1.0.0
pkgrel=1
pkgdesc="A GTK4/Adwaita system tool to manage CPU governor, I/O scheduler, and GPU performance profiles."
arch=('x86_64')
depends=('python-gobject' 'python-psutil' 'pyinstaller')
makedepends=('pyinstaller')
source=("git+https://github.com/franiekidos/antisos-finetuner.git")
sha256sums=('SKIP') # Replace with actual checksums later

# This package builds a self-contained executable using pyinstaller
build() {
  cd "${srcdir}/${pkgname}"
  
  # Assuming the main Python script is named 'antisos_performance_manager.py'
  /usr/bin/pyinstaller \
    --onefile \
    --name "${pkgname}" \
    --hiddenimport=gi.repository.Gtk \
    --hiddenimport=gi.repository.Adw \
    --hiddenimport=gi.repository.GLib \
    --hiddenimport=gi.repository.Gdk \
    --hiddenimport=gi.repository.Gio \
    antisos-finetuner
}

package() {
  # 1. Install the binary executable built by pyinstaller
  install -D -m755 "${srcdir}/dist/${pkgname}" "${pkgdir}/usr/bin/${pkgname}"
  
  # 2. Install the desktop file
  install -D -m644 "${srcdir}/${pkgname}.desktop" "${pkgdir}/usr/share/applications/${pkgname}.desktop"

  # 3. Optional: Install an icon (if you had one, e.g., in a $srcdir/ folder)
  # Since the app uses a built-in system icon ('preferences-system-symbolic'), we skip this.
  
  # 4. Create an entry point wrapper script to allow execution with arguments from the .desktop file actions.
  # This wrapper ensures the application can be executed directly or with profile arguments.
  # Note: The existing python script does not yet support CLI arguments, but this sets up the structure.
  
  # For the purpose of this example, we assume the Python script is updated to read sys.argv for profile.
  # If the Python file 'antisos_performance_manager.py' were available, we'd include it in $srcdir.
  # Since it's not present in this build context, we stick to the PyInstaller binary.
}