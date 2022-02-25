include ../Makefile.in

vector:
	$(CC) $(RVV) $(TOOLCHAIN) $(EXTRA_FLAGS_VECTOR) -c -o src/blackscholes.o src/blackscholes.cpp
	$(CC) $(RVV) $(TOOLCHAIN) $(EXTRA_FLAGS_VECTOR) $(LINK_FLAGS) -o $(target) src/*.o -lm

serial:
	$(CC) $(RVV) $(TOOLCHAIN) $(EXTRA_FLAGS_SERIAL) -c -o src/blackscholes.o src/blackscholes.cpp
	$(CC) $(RVV) $(TOOLCHAIN) $(EXTRA_FLAGS_SERIAL) $(LINK_FLAGS) -o $(target) src/*.o -lm

runspike :
	$(SPIKE) --isa=rv64gcv $(PK) $(target) 1 ./input/in_64K.input prices.txt
