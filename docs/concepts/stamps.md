## Stamps

A stamp is a single unit of computational work in a smart contract. Stamps are paid for with Xian. This is what enforces rate limiting and incentivizes the development of the network.

To calculate work, the code is ran through an optimized tracer. Each Python VM opcode has a specific cost. Each step of the code deducts from the number of stamps attached to the transaction.

If all of the stamps are deducted before the transaction is done, the transaction reverts states and fails. If there are left over stamps from the transaction execution, they are returned to the sender.

## Read Write Costs
* Cost to read one byte from state: 3 stamps
* Cost to write one byte to state: 25 stamps

## Opcode Cost Chart

Details on Python Opcodes from the `dis` module documentation [here](https://docs.python.org/3/library/dis.html). CPython Opcode definitions [here](https://github.com/python/cpython/blob/master/Include/opcode.h).

Not all opcodes in this list may ever be encountered in valid Contracting code.

|Op Code                                     |Num|Cost|Multiplier|Actual Cost|
|--------------------------------------------|---|----|----------|-----------|
|CACHE                                       |0  |1   |1         |1          |
|POP_TOP                                     |1  |1   |2         |2          |
|PUSH_NULL                                   |2  |1   |2         |2          |
|NOP                                         |9  |1   |2         |2          |
|UNARY_POSITIVE                              |10 |1   |2         |2          |
|UNARY_NEGATIVE                              |11 |2   |2         |4          |
|UNARY_NOT                                   |12 |1   |2         |2          |
|UNARY_INVERT                                |15 |2   |2         |4          |
|BINARY_SUBSCR                               |25 |2   |2         |4          |
|GET_LEN                                     |30 |2   |2         |4          |
|MATCH_MAPPING                               |31 |3   |2         |6          |
|MATCH_SEQUENCE                              |32 |3   |2         |6          |
|MATCH_KEYS                                  |33 |3   |2         |6          |
|PUSH_EXC_INFO                               |35 |3   |2         |6          |
|CHECK_EXC_MATCH                             |36 |3   |2         |6          |
|CHECK_EG_MATCH                              |37 |3   |2         |6          |
|WITH_EXCEPT_START                           |49 |3   |2         |6          |
|GET_AITER                                   |50 |3   |2         |6          |
|GET_ANEXT                                   |51 |3   |2         |6          |
|BEFORE_ASYNC_WITH                           |52 |3   |2         |6          |
|BEFORE_WITH                                 |53 |2   |2         |4          |
|END_ASYNC_FOR                               |54 |3   |2         |6          |
|STORE_SUBSCR                                |60 |2   |2         |4          |
|DELETE_SUBSCR                               |61 |2   |2         |4          |
|GET_ITER                                    |68 |4   |2         |8          |
|GET_YIELD_FROM_ITER                         |69 |6   |2         |12         |
|PRINT_EXPR                                  |70 |1   |2         |2          |
|LOAD_BUILD_CLASS                            |71 |805 |2         |1610       |
|LOAD_ASSERTION_ERROR                        |74 |2   |2         |4          |
|RETURN_GENERATOR                            |75 |3   |2         |6          |
|LIST_TO_TUPLE                               |82 |2   |2         |4          |
|RETURN_VALUE                                |83 |1   |2         |2          |
|IMPORT_STAR                                 |84 |63  |2         |126        |
|SETUP_ANNOTATIONS                           |85 |500 |2         |1000       |
|YIELD_VALUE                                 |86 |2   |2         |4          |
|ASYNC_GEN_WRAP                              |87 |4   |2         |8          |
|PREP_RERAISE_STAR                           |88 |3   |2         |6          |
|POP_EXCEPT                                  |89 |2   |2         |4          |
|HAVE_ARGUMENT                               |90 |1   |2         |2          |
|STORE_NAME                                  |90 |1   |2         |2          |
|DELETE_NAME                                 |91 |1   |2         |2          |
|UNPACK_SEQUENCE                             |92 |1   |2         |2          |
|FOR_ITER                                    |93 |4   |2         |8          |
|UNPACK_EX                                   |94 |4   |2         |8          |
|STORE_ATTR                                  |95 |3   |2         |6          |
|DELETE_ATTR                                 |96 |3   |2         |6          |
|STORE_GLOBAL                                |97 |2   |2         |4          |
|DELETE_GLOBAL                               |98 |2   |2         |4          |
|SWAP                                        |99 |1   |2         |2          |
|LOAD_CONST                                  |100|1   |2         |2          |
|LOAD_NAME                                   |101|1   |2         |2          |
|BUILD_TUPLE                                 |102|1   |2         |2          |
|BUILD_LIST                                  |103|3   |2         |6          |
|BUILD_SET                                   |104|4   |2         |8          |
|BUILD_MAP                                   |105|4   |2         |8          |
|LOAD_ATTR                                   |106|2   |2         |4          |
|COMPARE_OP                                  |107|2   |2         |4          |
|IMPORT_NAME                                 |108|19  |2         |38         |
|IMPORT_FROM                                 |109|63  |2         |126        |
|JUMP_FORWARD                                |110|2   |2         |4          |
|JUMP_IF_FALSE_OR_POP                        |111|2   |2         |4          |
|JUMP_IF_TRUE_OR_POP                         |112|2   |2         |4          |
|POP_JUMP_FORWARD_IF_FALSE                   |114|2   |2         |4          |
|POP_JUMP_FORWARD_IF_TRUE                    |115|2   |2         |4          |
|LOAD_GLOBAL                                 |116|2   |2         |4          |
|IS_OP                                       |117|2   |2         |4          |
|CONTAINS_OP                                 |118|3   |2         |6          |
|RERAISE                                     |119|3   |2         |6          |
|COPY                                        |120|2   |2         |4          |
|BINARY_OP                                   |122|2   |2         |4          |
|SEND                                        |123|3   |2         |6          |
|LOAD_FAST                                   |124|1   |2         |2          |
|STORE_FAST                                  |125|1   |2         |2          |
|DELETE_FAST                                 |126|1   |2         |2          |
|POP_JUMP_FORWARD_IF_NOT_NONE                |128|2   |2         |4          |
|POP_JUMP_FORWARD_IF_NONE                    |129|2   |2         |4          |
|RAISE_VARARGS                               |130|3   |2         |6          |
|CALL_FUNCTION                               |131|5   |2         |10         |
|MAKE_FUNCTION                               |132|4   |2         |8          |
|BUILD_SLICE                                 |133|6   |2         |12         |
|JUMP_BACKWARD_NO_INTERRUPT                  |134|2   |2         |4          |
|MAKE_CELL                                   |135|2   |2         |4          |
|LOAD_CLOSURE                                |136|4   |2         |8          |
|LOAD_DEREF                                  |137|1   |2         |2          |
|STORE_DEREF                                 |138|1   |2         |2          |
|DELETE_DEREF                                |139|1   |2         |2          |
|JUMP_BACKWARD                               |140|2   |2         |4          |
|CALL_FUNCTION_EX                            |142|6   |2         |12         |
|EXTENDED_ARG                                |144|1   |2         |2          |
|LIST_APPEND                                 |145|4   |2         |8          |
|SET_ADD                                     |146|4   |2         |8          |
|MAP_ADD                                     |147|3   |2         |6          |
|LOAD_CLASSDEREF                             |148|1   |2         |2          |
|COPY_FREE_VARS                              |149|3   |2         |6          |
|RESUME                                      |151|3   |2         |6          |
|MATCH_CLASS                                 |152|3   |2         |6          |
|FORMAT_VALUE                                |155|2   |2         |4          |
|BUILD_CONST_KEY_MAP                         |156|3   |2         |6          |
|BUILD_STRING                                |157|2   |2         |4          |
|LOAD_METHOD                                 |160|2   |2         |4          |
|LIST_EXTEND                                 |162|2   |2         |4          |
|SET_UPDATE                                  |163|3   |2         |6          |
|DICT_MERGE                                  |164|3   |2         |6          |
|DICT_UPDATE                                 |165|3   |2         |6          |
|PRECALL                                     |166|3   |2         |6          |
|CALL                                        |171|4   |2         |8          |
|KW_NAMES                                    |172|1   |2         |2          |
|POP_JUMP_BACKWARD_IF_NOT_NONE               |173|2   |2         |4          |
|POP_JUMP_BACKWARD_IF_NONE                   |174|2   |2         |4          |
|POP_JUMP_BACKWARD_IF_FALSE                  |175|2   |2         |4          |
|POP_JUMP_BACKWARD_IF_TRUE                   |176|2   |2         |4          |
|BINARY_OP_ADAPTIVE                          |3  |2   |2         |4          |
|BINARY_OP_ADD_FLOAT                         |4  |2   |2         |4          |
|BINARY_OP_ADD_INT                           |5  |2   |2         |4          |
|BINARY_OP_ADD_UNICODE                       |6  |2   |2         |4          |
|BINARY_OP_INPLACE_ADD_UNICODE               |7  |2   |2         |4          |
|BINARY_OP_MULTIPLY_FLOAT                    |8  |2   |2         |4          |
|BINARY_OP_MULTIPLY_INT                      |13 |2   |2         |4          |
|BINARY_OP_SUBTRACT_FLOAT                    |14 |2   |2         |4          |
|BINARY_OP_SUBTRACT_INT                      |16 |2   |2         |4          |
|BINARY_SUBSCR_ADAPTIVE                      |17 |2   |2         |4          |
|BINARY_SUBSCR_DICT                          |18 |2   |2         |4          |
|BINARY_SUBSCR_GETITEM                       |19 |2   |2         |4          |
|BINARY_SUBSCR_LIST_INT                      |20 |1   |2         |2          |
|BINARY_SUBSCR_TUPLE_INT                     |21 |1   |2         |2          |
|CALL_ADAPTIVE                               |22 |4   |2         |8          |
|CALL_PY_EXACT_ARGS                          |23 |3   |2         |6          |
|CALL_PY_WITH_DEFAULTS                       |24 |3   |2         |6          |
|COMPARE_OP_ADAPTIVE                         |26 |2   |2         |4          |
|COMPARE_OP_FLOAT_JUMP                       |27 |2   |2         |4          |
|COMPARE_OP_INT_JUMP                         |28 |2   |2         |4          |
|COMPARE_OP_STR_JUMP                         |29 |2   |2         |4          |
|EXTENDED_ARG_QUICK                          |34 |1   |2         |2          |
|JUMP_BACKWARD_QUICK                         |38 |1   |2         |2          |
|LOAD_ATTR_ADAPTIVE                          |39 |2   |2         |4          |
|LOAD_ATTR_INSTANCE_VALUE                    |40 |2   |2         |4          |
|LOAD_ATTR_MODULE                            |41 |2   |2         |4          |
|LOAD_ATTR_SLOT                              |42 |2   |2         |4          |
|LOAD_ATTR_WITH_HINT                         |43 |2   |2         |4          |
|LOAD_CONST__LOAD_FAST                       |44 |1   |2         |2          |
|LOAD_FAST__LOAD_CONST                       |45 |1   |2         |2          |
|LOAD_FAST__LOAD_FAST                        |46 |1   |2         |2          |
|LOAD_GLOBAL_ADAPTIVE                        |47 |2   |2         |4          |
|LOAD_GLOBAL_BUILTIN                         |48 |1   |2         |2          |
|LOAD_GLOBAL_MODULE                          |55 |2   |2         |4          |
|LOAD_METHOD_ADAPTIVE                        |56 |2   |2         |4          |
|LOAD_METHOD_CLASS                           |57 |2   |2         |4          |
|LOAD_METHOD_MODULE                          |58 |2   |2         |4          |
|LOAD_METHOD_NO_DICT                         |59 |2   |2         |4          |
|LOAD_METHOD_WITH_DICT                       |62 |2   |2         |4          |
|LOAD_METHOD_WITH_VALUES                     |63 |2   |2         |4          |
|PRECALL_ADAPTIVE                            |64 |3   |2         |6          |
|PRECALL_BOUND_METHOD                        |65 |3   |2         |6          |
|PRECALL_BUILTIN_CLASS                       |66 |4   |2         |8          |
|PRECALL_BUILTIN_FAST_WITH_KEYWORDS          |67 |4   |2         |8          |
|PRECALL_METHOD_DESCRIPTOR_FAST_WITH_KEYWORDS|72 |4   |2         |8          |
|PRECALL_NO_KW_BUILTIN_FAST                  |73 |3   |2         |6          |
|PRECALL_NO_KW_BUILTIN_O                     |76 |3   |2         |6          |
|PRECALL_NO_KW_ISINSTANCE                    |77 |2   |2         |4          |
|PRECALL_NO_KW_LEN                           |78 |2   |2         |4          |
|PRECALL_NO_KW_LIST_APPEND                   |79 |2   |2         |4          |
|PRECALL_NO_KW_METHOD_DESCRIPTOR_FAST        |80 |3   |2         |6          |
|PRECALL_NO_KW_METHOD_DESCRIPTOR_NOARGS      |81 |3   |2         |6          |
|PRECALL_NO_KW_METHOD_DESCRIPTOR_O           |113|3   |2         |6          |
|PRECALL_NO_KW_STR_1                         |121|2   |2         |4          |
|PRECALL_NO_KW_TUPLE_1                       |127|2   |2         |4          |
|PRECALL_NO_KW_TYPE_1                        |141|3   |2         |6          |
|PRECALL_PYFUNC                              |143|3   |2         |6          |
|RESUME_QUICK                                |150|3   |2         |6          |
|STORE_ATTR_ADAPTIVE                         |153|2   |2         |4          |
|STORE_ATTR_INSTANCE_VALUE                   |154|2   |2         |4          |
|STORE_ATTR_SLOT                             |158|2   |2         |4          |
|STORE_ATTR_WITH_HINT                        |159|2   |2         |4          |
|STORE_FAST__LOAD_FAST                       |161|1   |2         |2          |
|STORE_FAST__STORE_FAST                      |167|1   |2         |2          |
|STORE_SUBSCR_ADAPTIVE                       |168|2   |2         |4          |
|STORE_SUBSCR_DICT                           |169|2   |2         |4          |
|STORE_SUBSCR_LIST_INT                       |170|1   |2         |2          |
|UNPACK_SEQUENCE_ADAPTIVE                    |177|2   |2         |4          |
|UNPACK_SEQUENCE_LIST                        |178|2   |2         |4          |
|UNPACK_SEQUENCE_TUPLE                       |179|2   |2         |4          |
|UNPACK_SEQUENCE_TWO_TUPLE                   |180|2   |2         |4          |
|DO_TRACING                                  |255|4   |2         |8          |
|NB_ADD                                      |0  |1   |2         |2          |
|NB_SUBTRACT                                 |10 |1   |2         |2          |
|NB_MULTIPLY                                 |5  |1   |2         |2          |
|NB_AND                                      |1  |1   |2         |2          |
|NB_OR                                       |7  |1   |2         |2          |
|NB_XOR                                      |12 |1   |2         |2          |
|NB_LSHIFT                                   |3  |1   |2         |2          |
|NB_RSHIFT                                   |9  |1   |2         |2          |
|NB_INPLACE_ADD                              |13 |1   |2         |2          |
|NB_INPLACE_SUBTRACT                         |23 |1   |2         |2          |
|NB_INPLACE_MULTIPLY                         |18 |1   |2         |2          |
|NB_INPLACE_AND                              |14 |1   |2         |2          |
|NB_INPLACE_OR                               |20 |1   |2         |2          |
|NB_INPLACE_XOR                              |25 |1   |2         |2          |
|NB_INPLACE_LSHIFT                           |16 |1   |2         |2          |
|NB_INPLACE_RSHIFT                           |22 |1   |2         |2          |
|NB_TRUE_DIVIDE                              |11 |2   |2         |4          |
|NB_FLOOR_DIVIDE                             |2  |2   |2         |4          |
|NB_REMAINDER                                |6  |2   |2         |4          |
|NB_POWER                                    |8  |2   |2         |4          |
|NB_INPLACE_TRUE_DIVIDE                      |24 |2   |2         |4          |
|NB_INPLACE_FLOOR_DIVIDE                     |15 |2   |2         |4          |
|NB_INPLACE_REMAINDER                        |19 |2   |2         |4          |
|NB_INPLACE_POWER                            |21 |2   |2         |4          |
|NB_MATRIX_MULTIPLY                          |17 |2   |2         |4          |
|NB_INPLACE_MATRIX_MULTIPLY                  |17 |2   |2         |4          |

