# set the list of all test routines to compile
TESTSOURCES = lvect_bench.cpp lvect_bench_nompi.cpp test_synch.cpp #test_cxx.cpp # stream.c # test_f90.f90

# set test specific compiler and linker options
TESTCXXFLAGS = -I$(top_srcdir) @PAPI_CFLAGS@
TESTLDFLAGS  = @PAPI_LDFLAGS@
TESTLIBS     = $(top_builddir)/.libs/liblsb-0.2.a

# this ensure that test cases and verified outputs will be distributed
EXTRA_DIST = $(TESTSOURCES) 

TESTCXXCOMPILE = $(CXX) $(DEFS) $(DEFAULT_INCLUDES) $(INCLUDES) $(CPPFLAGS) $(CXXFLAGS) $(TESTCXXFLAGS)
TESTCXXLINK = $(CXX) $(AM_CXXFLAGS) $(CXXFLAGS) $(AM_LDFLAGS) $(LDFLAGS) $(TESTLDFLAGS) -o $@ 

TESTBINS_CPP=$(TESTSOURCES:.cpp=.test)
TESTBINS_F90=$(TESTSOURCES:.f90=.test)

tests: $(TESTBINS_CPP) $(TESTBINS_F90)

.cpp.test:
	$(TESTCXXCOMPILE) -c -o $*.o $<
	$(TESTCXXLINK) $*.o $(TESTLIBS)  
	./$*.test

.f90.test:
	$(TESTF90COMPILE) -c -o $*.o $<
	$(TESTF90LINK) $*.o $(TESTLIBS) 
	./$*.test

	
clean-local:
	$(RM) -rf $(TESTSOURCES:.cpp=.test) $(TESTSOURCES:.cpp=.o) \
	    $(TESTSOURCES:.cpp=.lastout) $(TESTSOURCES:.cpp=.diff)

