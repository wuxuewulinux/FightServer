
#有多少个proto协议文件就要在这里增加一样的命令
$(shell rm *.pb.h *.pb.cc)
$(shell rm ../dep/*.pb.d ../link_obj/*.pb.o)
$(shell protoc --cpp_out=. CSmsg.proto)
$(shell protoc --cpp_out=. SSmsg.proto)
$(shell protoc --cpp_out=. DBmsg.proto)
.PHONY:all
SRCS = $(wildcard *.cc)
OBJS = $(SRCS:.cc=.o)
DEPS = $(SRCS:.cc=.d)
#BIN := $(addprefix /home/wuxuewu/fuwuqi/base/,$(BIN))

LINK_OBJ_DIR = /home/wuxuewu/FightServer/link_obj
$(shell mkdir -p $(LINK_OBJ_DIR))

DEP_DIR = /home/wuxuewu/FightServer/dep
$(shell mkdir -p $(DEP_DIR))

OBJS := $(addprefix $(LINK_OBJ_DIR)/,$(OBJS))
DEPS := $(addprefix $(DEP_DIR)/,$(DEPS))
LINK_OBJ = $(wildcard $(LINK_OBJ_DIR)/*.o)
LINK_OBJ +=$(OBJS)
all: $(DEPS) $(OBJS) $(BIN)
ifneq ("$(wildcard $(DEPS))","")
include $(DEPS)
endif
#$(BIN):$(LINK_OBJ)
$(LINK_OBJ_DIR)/%.o:%.cc
	g++ -o $@ -c $(filter %.cc,$^)
$(DEP_DIR)/%.d:%.cc
	gcc -MM $(filter %.cc,$^) | sed 's,\(.*\).o[ :]*,$(LINK_OBJ_DIR)/\1.o $@:,g' > $@


