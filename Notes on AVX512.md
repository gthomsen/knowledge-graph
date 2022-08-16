Tags: #software-engineering #compiler-optimizations #scientific-computing 

AVX-512 doubled the vector width (to 16x 32-bit floats and 8x 64-bit doubles) and increased the register count to 32.  There are 8 opmask registers for masked instructions.

# Vector Length Extentions (VLE)
Vector Length Extensions allow use of AVX-512 instructions on shorter vector lengths: 128-bit registers (XMM) and 256-bit registers (YMM), on top of 512-bit registers (ZMM).