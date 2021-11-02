pkgname=wasi-sdk-git
pkgver=r121.77ba98a
pkgrel=1
pkgdesc="WASI-enabled WebAssembly C/C++ toolchain (from git repo)"
arch=("x86_64")
license=('Apache')
depends=(clang lld)
makedepends=(cmake ninja python git)
source=('git+https://github.com/WebAssembly/wasi-sdk.git'
        'git+https://git.savannah.gnu.org/git/config.git'
        'git+https://github.com/llvm/llvm-project.git'
        'git+https://github.com/WebAssembly/wasi-libc.git')
md5sums=('SKIP'
         'SKIP'
         'SKIP'
         'SKIP')
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
options=('!strip' 'staticlibs')

prepare() {
  cd "$srcdir/${pkgname%-git}"
  git submodule init
  git config submodule.src/config.url "$srcdir/config"
  git config submodule.src/llvm-project.url "$srcdir/llvm-project"
  git config submodule.src/wasi-libc.url "$srcdir/wasi-libc"
  git submodule update
}

pkgver() {
  cd "$srcdir/${pkgname%-git}"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
  cd "$srcdir/${pkgname%-git}"
  make \
    PREFIX=/opt/wasi-sdk \
    DESTDIR="$pkgdir" \
    build/wasi-libc.BUILT \
    build/libcxx.BUILT \
    build/libcxxabi.BUILT
}

package() {
    true
}
