ifneq ($(words $(CURDIR)),1)
 $(error Unsupported: GNU Make cannot build in directories containing spaces, build elsewhere: '$(CURDIR)')
endif

ifeq ($(VERILATOR_ROOT),)
VERILATOR = verilator
else
export VERILATOR_ROOT
VERILATOR = $(VERILATOR_ROOT)/bin/verilator
endif

default:
	@echo "-- Verilator bus read/write example"
	@echo "-- VERILATE ----------------"
	$(VERILATOR) -cc top.v --exe -CFLAGS "-Wpedantic -Wall" sim_main.cpp ../../src/renode.cpp ../../src/buses/axilite.cpp ../../src/peripherals/uart.cpp
	@echo "-- COMPILE -----------------"
	LDLIBS="-lzmq -lpthread" $(MAKE) -j 4 -C obj_dir -f Vtop.mk

maintainer-copy::
clean mostlyclean distclean maintainer-clean::
	-rm -rf obj_dir *.log *.dmp *.vpd core
