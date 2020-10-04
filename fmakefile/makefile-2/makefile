# Makefile này được thực hiện với điều kiện makefile và file main nằm cùng thư mục, còn các file nguồn, file header và file src.mk nằm trong thư mục src cùng cấp với file main
# Sơ đồ filw:
# -src/
# --(các file nguồn và header)
# -main.c (hoặc main.cpp)
# -makefile




# Lệnh make đầu tiên. Ở đây không xoá file thực thi cũng như không cài đặt vào máy nên không cần install và clean
.PHONY: all, run

# Tên chương trình cần tạo ra:
TARGET:= 

# include makefile phụ vào makefile chính:
-include ./src/src.mk

# Nếu file main là file C thì đặt main.c ở đây:
CSRCS+= main.c

# Nếu file main là file C++ thì đặt main.cpp ở đây:
CPPSRCS+= 


Thư mục chứa các file object
OBJSDIR=./buid

OBJS:= $(patsubst %.c, $(OBJSDIR)/%.o, $(CSRCS))
OBJS+= $(patsubst %.cpp, $(OBJSDIR)/%.o, $(CPPSRCS))

# Thư mục chứa các file include vào file main:
INCDIR+= -I./src

# Các flag chứa các tuỳ chọn để pass vào compiler:
CFLAGS+= -DDEBUG -Wall -g
LDFLAGS+= -L./lib -lm

# Sử dụng gcc làm trình biên dịch C và g++ làm trình biên dịch C++
CC:= gcc
CXX:= g++

# Lệnh make đầu tiên, tạo file $(TARGET) từ các file object:
all: ${TARGET}
${TARGET}: $(OBJS)
	@echo " [LINK] $@"
	@mkdir -p $(shell dirname $@)
	@$(CXX) $(OBJS) -o $@ $(LDFLAGS)

# Nếu các file object chưa được tạo hoặc đã bị thay đổi thì sẽ tạo file object:

# Tạo các file object từ các file C:
$(OBJSDIR)/%.o: %.c $(HDRS)
	@echo " [CC] $@"
	@mkdir -p $(shell dirname $@)
	@$(CC) -c $< -o $@ $(CFLAGS) ${INCDIR}

# Tạo các file object từ các file C++
$(OBJSDIR)/%.o: %.cpp $(HDRS)
	@echo "[CXX] $@"
	@mkdir -p $(shell dirname $@)
	@$(CXX) -c $< -o $@ $(CFLAGS) ${INCDIR}

# Lệnh cài đặt chương trình vào thư mục chứa các file thực thi của người dùng:
# Nếu không muốn cài đặt thì bỏ "install" trong các tham số của lệnh ".PHONY"
install:
	cp -rf ${TARGET} /usr/local/bin

# Lệnh xoá file chương trình vừa được tạo ra và thư mục chứa các file object:
clean:
	rm -rf ${OBJSDIR}
	rm -rf ${TARGET}

# Lệnh chạy file chương trình sau khi được tạo ra hoặc sửa đổi:
run:
	./${TARGET}