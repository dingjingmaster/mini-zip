cmake_minimum_required(VERSION 3.10)
project(mini-zip)

set(CMAKE_CXX_STANDARD 11)

file(GLOB MINI_ZIP_SRC
        # core file
        mz_os.c
        mz_zip.c
        mz_strm.c
        mz_crypt.c
        mz_zip_rw.c
        mz_strm_buf.c
        mz_strm_mem.c
        mz_crypt_brg.c
        mz_strm_split.c

        mz_os_posix.c
        mz_compat.c

        mz_strm_bzip.c
        mz_strm_pkcrypt.c
        mz_strm_os_posix.c
#        mz_strm_wzaes.c
#        mz_strm_pkcrypt.c


        lib/brg/sha1.c
        lib/brg/sha2.c
        lib/brg/hmac.c
        lib/brg/aestab.c
        lib/brg/aeskey.c
        lib/brg/aescrypt.c

        lib/bzip2/bzlib.c
        lib/bzip2/huffman.c
        lib/bzip2/compress.c
        lib/bzip2/crctable.c
        lib/bzip2/blocksort.c
        lib/bzip2/randtable.c
        lib/bzip2/decompress.c
)

add_executable(mini-zip main.c ${MINI_ZIP_SRC})
target_include_directories(mini-zip PUBLIC lib/brg)
target_compile_definitions(mini-zip PUBLIC
        -DHAVE_BZIP2
        -DMZ_ZIP_SIGNING
        -DHAVE_PKCRYPT
)
