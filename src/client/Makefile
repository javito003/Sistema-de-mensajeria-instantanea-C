MAIN_SRC=client.c
SOURCES=chats.c friends.c messages.c chat_members.c friend_requests.c persistence.c psd_ims_client.c network.c client_graphic_v2.c
HEADERS=chats.h friends.h messages.h chat_members.h friend_requests.h persistence.h psd_ims_client.h network.h client_graphic_v2.h

COMMON_LIBS=list leak_detector_c
RPC_LIBS=soapC soapClient

TARGET=$(MAIN_SRC:%.c=$(BIN_DIR)/%)
TEST_LIB=$(MAIN_SRC:%.c=$(OBJ_DIR)/lib%.a)
MAIN_OBJ=$(MAIN_SRC:%.c=$(MAIN_OBJ_DIR)/%.o)
COBJS=$(SOURCES:%.c=$(OBJ_DIR)/%.o)
COMMON_OBJS=$(COMMON_LIBS:%=$(OBJ_COMMON_DIR)/%.o)
RPC_OBJS=$(RPC_LIBS:%=$(OBJ_RPC_DIR)/%.o)
CHEADS=$(HEADERS)

ECHO_FLAGS=

#-------------------------------------------------------------
# Directories
#-------------------------------------------------------------
PROJECT_DIR=../..
SUBPROJECT=client
SRC_DIR=$(PROJECT_DIR)/src/$(SUBPROJECT)
SRC_COMMON_DIR=$(PROJECT_DIR)/src/common
SRC_RPC_DIR=$(PROJECT_DIR)/src/rpc
OBJ_DIR=$(PROJECT_DIR)/build/$(SUBPROJECT)
MAIN_OBJ_DIR=$(PROJECT_DIR)/build/$(SUBPROJECT)/$(SUBPROJECT)
OBJ_COMMON_DIR=$(PROJECT_DIR)/build/common
OBJ_RPC_DIR=$(PROJECT_DIR)/build/rpc
BIN_DIR=$(PROJECT_DIR)/bin



#-------------------------------------------------------------
# Configuration
#-------------------------------------------------------------
CFLAGS=-I$(SRC_COMMON_DIR) -I$(SRC_RPC_DIR) -I$(GSOAP_INCLUDE)
LDFLAGS=-L$(GSOAP_LIB)
LDLIBS=-lgsoap $(SSL_LIBS) -pthread

SSL_LIBS=-lssl -lcrypto
SSL_FLAGS=-DWITH_OPENSSL

#gcc $(SSL_FLAGS) -o $(CLIENT) $(CLIENT_SRC) -I$(GSOAP_INCLUDE) -lgsoap $(SSL_LIBS) -L$(GSOAP_LIB)

all: $(TARGET)

$(TARGET): $(BIN_DIR) $(OBJ_DIR) $(MAIN_OBJ_DIR) $(COMMON_OBJS) $(COBJS) $(MAIN_OBJ)
	@echo $(ECHO_FLAGS) "\tLD " $(TARGET)	
	@gcc -o $@ $(MAIN_OBJ) $(COBJS) $(COMMON_OBJS) $(RPC_OBJS) $(LDFLAGS) $(SSL_FLAGS) $(LDLIBS)
	

$(MAIN_OBJ_DIR)/%.o : %.c
	@echo $(ECHO_FLAGS) "\tCC" $@
	@gcc -c -o $@ $< $(CFLAGS) $(EXTRA_CFLAGS)
	

$(OBJ_DIR)/%.o : %.c
	@echo $(ECHO_FLAGS) "\tCC" $@
	@gcc -c -o $@ $< $(CFLAGS) $(EXTRA_CFLAGS)


$(COBJS): | $(OBJ_DIR) $(MAIN_OBJ_DIR)

$(TARGET): | $(BIN_DIR)

clean:
	@rm -rf *.xml *.nsmap *.wsdl *.xsd
	@rm -rf soap*

#------------------------------------------------------------------------------------
#		Directories 
#------------------------------------------------------------------------------------

$(OBJ_DIR):
	@echo $(ECHO_FLAGS) "\tCreating dir $(OBJ_DIR)"
	@mkdir -p $(OBJ_DIR)

$(MAIN_OBJ_DIR):
	@echo $(ECHO_FLAGS) "\tCreating dir $(MAIN_OBJ_DIR)"
	@mkdir -p $(MAIN_OBJ_DIR)

$(BIN_DIR):
	@echo $(ECHO_FLAGS) "\tCreating dir $(BIN_DIR)"
	@mkdir -p $(BIN_DIR)

