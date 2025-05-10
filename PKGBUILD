# Maintainer: txtsd <aur.archlinux@ihavea.quest>

pkgname=llama.cpp-cuda-git
pkgver=b5338
pkgrel=1
pkgdesc="Port of Facebook's LLaMA model in C/C++"
arch=(x86_64 armv7h aarch64)
url='https://github.com/ggml-org/llama.cpp'
license=('MIT')
depends=(
  curl
  gcc-libs
  glibc
  python
  python-numpy
)
makedepends=(
  cmake
  git
  openmp
)
optdepends=(python-pytorch)
options+=(lto)
source=(
  "git+${url}"
  llama.cpp.conf
  llama.cpp.service
)
sha256sums=('SKIP'
            'SKIP'
            'SKIP')


build() {
  local _cmake_options=(
    -B build
    -S "llama.cpp"
    -DCMAKE_BUILD_TYPE=None
    -DCMAKE_INSTALL_PREFIX='/usr'
    -DGGML_ALL_WARNINGS=OFF
    -DGGML_ALL_WARNINGS_3RD_PARTY=OFF
    -DBUILD_SHARED_LIBS=ON
    -DGGML_STATIC=OFF
    -DGGML_LTO=ON
    -DGGML_RPC=ON
    -DGGML_CUDA=ON
    -DLLAMA_CURL=ON
    -DGGML_BLAS=OFF
    -Wno-dev
  )
  cmake "${_cmake_options[@]}"
  cmake --build build
}

# check() {
#   ctest --test-dir build --output-on-failure -L 'main|curl' --verbose --timeout 900
# }

package() {
  DESTDIR="${pkgdir}" cmake --install build
  rm "${pkgdir}/usr/include/"ggml*

  install -Dm644 "llama.cpp/LICENSE" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"

  install -Dm644 "llama.cpp.conf" "${pkgdir}/etc/conf.d/llama.cpp"
  install -Dm644 "llama.cpp.service" "${pkgdir}/usr/lib/systemd/system/llama.cpp.service"
}
