# Makefile này thực hiện với điều kiện file main, các file thư viện và makefile nằm trong cùng thư mục






# Lệnh make đầu tiên. Ở đây không xoá file thực thi cũng như không cài đặt vào máy nên không cần install và clean
.PHONY: all, run

# Tên chương trình cần tạo ra
TARGET=

# Thêm thư viện tại đây:
HDRS+= 

# Thêm file .c tại đây:
CSRCS+= 

# Thêm file .cpp tại đây:
CPPSRCS+= 


# Thư mục chứa file object:
OBJSDIR=./build

OBJS:= $(patsubst %.c, $(OBJSDIR)/%.o, $(CSRCS))
OBJS+= $(patsubst %.cpp, $(OBJSDIR)/%.o, $(CPPSRCS))

CFLAGS+= -I./include -DDEBUG -Wall -g
LDFLAGS+= -L./lib -lm

CC:= gcc
CXX:= g++

all: ${TARGET}

${TARGET}: $(OBJS)
	@echo " [LINK] $@"
	@mkdir -p $(shell dirname $@)
	@$(CXX) $(OBJS) -o $@ $(LDFLAGS)

$(OBJSDIR)/%.o: %.c $(HDRS)
	@echo " [CC] $@"
	@mkdir -p $(shell dirname $@)
	@$(CC) -c $< -o $@ $(CFLAGS)

$(OBJSDIR)/%.o: %.cpp $(HDRS)
	@ehco " [CC] $@"
	@mkdir -p $(shell dirname $@)
	@$(CXX) -c $< -o $@ $(CFLAGS)

install:
	cp -rf ${TARGET} /usr/local/bin

clean:
	rm -rf $(OBJSDIR)/*.o
	rm -rf ${TARGET}

run:
	./${TARGET}