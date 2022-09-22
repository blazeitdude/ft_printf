GREEN = \033[0;32m
RED = \033[0;31m
RESET = \033[0m

NAME	= 	libftprintf.a
SRC_DIR	=	./sources/
SRC_L	=	ft_printf.c		\
			printf_utils.c

OBJ_D	=	objects/
OBJ_L	=	$(patsubst %.c, %.o, $(SRC_L))
OBJ	=	$(addprefix $(OBJ_D), $(OBJ_L))

INCLD	=	-I$(HEAD_D)
HEAD_L	=	ft_printf.h
HEAD_D	=	./includes/
HEADERS	=	$(addprefix $(HEAD_D), $(HEAD_L))

CC	=	gcc
CFLAGS	=	-Wall -Wextra -Werror -c
RM	=	rm -f


SRC_COUNT_TOT := $(shell expr $(shell echo -n $(SRC_L) | wc -w) - $(shell ls -l $(OBJ_D) 2>&1 | grep ".o" | wc -l) + 1)
ifeq ($(shell test $(SRC_COUNT_TOT) -le 0; echo $$?),0)
	SRC_COUNT_TOT := $(shell echo -n $(SRC) | wc -w)
endif
SRC_COUNT	:= 1
SRC_PCT = $(shell expr 100 \* $(SRC_COUNT) / $(SRC_COUNT_TOT))
PRINTF = LC_NUMERIC="en_US.UTF-8" printf


all	:	$(NAME)

$(NAME)	:	$(OBJ_D) $(OBJ)
	@ar rcs $(NAME) $(OBJ)
	@echo "\n$(NAME): $(GREEN)object files were created$(RESET)"
	@echo "$(NAME): $(GREEN)$(NAME) was created$(RESET)"


$(OBJ_D):
	@mkdir -p $(OBJ_D)
	@echo "$(NAME): $(GREEN)$(OBJ_D) was created$(RESET)"
$(OBJ_D)%.o	:	$(SRC_DIR)%.c $(HEADERS)
	@$(CC) $(CFLAGS) $(INCLD) $< -o $@
	@$(eval SRC_COUNT = $(shell expr $(SRC_COUNT) + 1))
	@$(PRINTF) "\r%100s\r[ %d/%d (%d%%) ] Compiling $(GREEN)$<$(RESET)..." "" $(SRC_COUNT) $(SRC_COUNT_TOT) $(SRC_PCT)

clean:
	@rm -rf $(OBJ_D)
	@echo "$(NAME): $(RED)$(OBJ_D) was deleted$(RESET)"
	@echo "$(NAME): $(RED)object files were deleted$(RESET)"

fclean: clean
	@rm -f $(NAME)
	@echo "$(NAME): $(RED)$(NAME) was deleted$(RESET)"

re:
	@$(MAKE) fclean
	@$(MAKE) all