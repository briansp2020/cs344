HIPCC=hipcc

###################################
# These are the default install   #
# locations on most linux distros #
###################################

OPENCV_LIBPATH=/usr/lib
OPENCV_INCLUDEPATH=/usr/include

###################################################
# On Macs the default install locations are below #
###################################################

#OPENCV_LIBPATH=/usr/local/lib
#OPENCV_INCLUDEPATH=/usr/local/include

# or if using MacPorts

#OPENCV_LIBPATH=/opt/local/lib
#OPENCV_INCLUDEPATH=/opt/local/include

OPENCV_LIBS=-lopencv_core -lopencv_imgproc -lopencv_highgui

HIP_INCLUDEPATH=/opt/rocm/hcc/include

######################################################
# On Macs the default install locations are below    #
# ####################################################

#CUDA_INCLUDEPATH=/usr/local/cuda/include
#CUDA_LIBPATH=/usr/local/cuda/lib

HIPCC_OPTS=-O2 -hc -std=c++amp

student: main.o student_func.o compare.o reference_calc.o Makefile
	$(HIPCC) -o HW1 main.o student_func.o compare.o reference_calc.o -L $(OPENCV_LIBPATH) $(OPENCV_LIBS) $(HIPCC_OPTS)

main.o: main.cpp timer.h utils.h reference_calc.cpp compare.cpp HW1.cpp
	$(HIPCC) -c main.cpp $(HIPCC_OPTS) -I $(HIP_INCLUDEPATH) -I $(OPENCV_INCLUDEPATH)

student_func.o: student_func.cpp utils.h
	$(HIPCC) -c student_func.cpp $(HIPCC_OPTS)

compare.o: compare.cpp compare.h
	$(HIPCC) -c compare.cpp -I $(OPENCV_INCLUDEPATH) $(HIPCC_OPTS)

reference_calc.o: reference_calc.cpp reference_calc.h
	$(HIPCC) -c reference_calc.cpp -I $(OPENCV_INCLUDEPATH) $(HIPCC_OPTS)

clean:
	rm -f *.o *.png hw
