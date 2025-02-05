# Compiler and Flags
NVCC            = nvcc
ARCH_FLAGS      = -arch=sm_86

# Build Flags
DEBUG_FLAGS     = -lineinfo
RELEASE_FLAGS   = -O3 -DNDEBUG

# Linking
# Uncomment and set these paths if needed
# SILO_INCLUDES  := /usr/local/silo-4.8/include
# SILO_LIBS      := /usr/local/silo-4.8/lib
# LINKFLAGS      += -L$(SILO_LIBS) -lsilo
LINKFLAGS       = 

# Source Directory
SRC_DIR         = ../src

# Include paths (uncomment if SILO_INCLUDES is used)
# INC_SILO       := -I$(SILO_INCLUDES)

# Targets
all: release

release: FLAGS = $(RELEASE_FLAGS)
debug:   FLAGS = $(DEBUG_FLAGS)

release: lulesh
debug: lulesh

# Rules
lulesh: allocator.o lulesh.o lulesh-comms.o lulesh-comms-gpu.o
	$(NVCC) $(LINKFLAGS) $^ -o $@

allocator.o: $(SRC_DIR)/allocator.cu $(SRC_DIR)/vector.h
	$(NVCC) $(FLAGS) $(ARCH_FLAGS) -I$(SRC_DIR) -c $< -o $@

lulesh.o: $(SRC_DIR)/lulesh.cu $(SRC_DIR)/util.h $(SRC_DIR)/vector.h $(SRC_DIR)/allocator.h
	$(NVCC) $(FLAGS) $(ARCH_FLAGS) -I$(SRC_DIR) $(INC_SILO) -c $< -o $@

lulesh-comms.o: $(SRC_DIR)/lulesh-comms.cu
	$(NVCC) $(FLAGS) $(ARCH_FLAGS) -I$(SRC_DIR) -c $< -o $@

lulesh-comms-gpu.o: $(SRC_DIR)/lulesh-comms-gpu.cu
	$(NVCC) $(FLAGS) $(ARCH_FLAGS) -I$(SRC_DIR) -c $< -o $@

clean:
	rm -f *.o lulesh xyz.asc regNumList.txt
