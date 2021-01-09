# Gramática Ascendente
```xml
<root> ::= <instructionlist>
       
<instructionlist> ::= <instructionlist> <sqlinstruction>
                    | <sqlinstruction>

<sqlinstruction> ::= <DDL>
                   | <DML>
                   | <usestatement>
                   | MULTI_LINE_COMMENT
                   | SINGLE_LINE_COMMENT
                   | <SQL_FUNCTION>
                   | <SQL_DROP_FUNCTION>
                   | <SQL_DROP_PROCEDURE>
                   | <SQL_PROCEDURES>
                   | <INDEXES_STATEMENT>
                   | <CALL_FUNCTIONS_PROCEDURE> SEMICOLON

<usestatement> ::= USE ID SEMICOLON

<DDL> ::= <createstatement>
        | <showstatement>
        | <alterstatement>
        | <dropstatement>

<createstatement> ::= CREATE <optioncreate> SEMICOLON      

<optioncreate> ::= <TYPE> <SQLNAME> AS ENUM LEFT_PARENTHESIS <typelist> RIGHT_PARENTHESIS
               	 | DATABASE <createdb>
               	 | OR REPLACE DATABASE <createdb>
               	 | TABLE <SQLNAME> LEFT_PARENTHESIS <columnstable> RIGHT_PARENTHESIS
               	 | TABLE <SQLNAME> LEFT_PARENTHESIS <columnstable> RIGHT_PARENTHESIS INHERITS LEFT_PARENTHESIS ID RIGHT_PARENTHESIS

<typelist> ::= <typelist> COMMA <SQLNAME>
             | <SQLNAME> 

<createdb> ::= IF NOT EXISTS ID <listpermits>
             | IF NOT EXISTS ID
             | ID <listpermits>
             | ID    

<listpermits> ::= <listpermits> <permits>
                | <permits>

<permits> ::= OWNER EQUALS SQLNAME
            | OWNER SQLNAME
            | MODE EQUALS INT_NUMBER
            | MODE INT_NUMBER  

<columnstable> ::= <columnstable> COMMA <column>
                 | <column>

<column> ::= ID <typecol> <optionscollist>
           | ID <typecol>
           | UNIQUE LEFT_PARENTHESIS <columnlist> RIGHT_PARENTHESIS
           | PRIMARY KEY LEFT_PARENTHESIS <columnlist> RIGHT_PARENTHESIS
           | FOREIGN KEY LEFT_PARENTHESIS <columnlist> RIGHT_PARENTHESIS REFERENCES ID LEFT_PARENTHESIS <columnlist> RIGHT_PARENTHESIS
           | CONSTRAINT ID CHECK LEFT_PARENTHESIS <conditionColumn> RIGHT_PARENTHESIS
           | CHECK LEFT_PARENTHESIS <conditionColumn> RIGHT_PARENTHESIS

<typecol> ::= SMALLINT
            | INTEGER
            | BIGINT
            | DECIMAL LEFT_PARENTHESIS INT_NUMBER COMMA INT_NUMBER RIGHT_PARENTHESIS
            | DECIMAL LEFT_PARENTHESIS INT_NUMBER RIGHT_PARENTHESIS
            | NUMERIC LEFT_PARENTHESIS INT_NUMBER COMMA INT_NUMBER RIGHT_PARENTHESIS
            | NUMERIC LEFT_PARENTHESIS INT_NUMBER RIGHT_PARENTHESIS
            | REAL
            | DOUBLE PRECISION
            | MONEY
            | CHARACTER VARYING LEFT_PARENTHESIS INT_NUMBER RIGHT_PARENTHESIS
            | CHARACTER VARYING
            | VARCHAR LEFT_PARENTHESIS INT_NUMBER RIGHT_PARENTHESIS
            | VARCHAR
            | CHARACTER LEFT_PARENTHESIS INT_NUMBER RIGHT_PARENTHESIS
            | CHARACTER
            | CHAR LEFT_PARENTHESIS INT_NUMBER RIGHT_PARENTHESIS
            | CHAR
            | TEXT
            | TIMESTAMP LEFT_PARENTHESIS INT_NUMBER RIGHT_PARENTHESIS
            | TIMESTAMP
            | DATE
            | TIME LEFT_PARENTHESIS INT_NUMBER RIGHT_PARENTHESIS
            | TIME
            | INTERVAL <SQLNAME>
            | BOOLEAN               

<optionscollist> ::= <optionscollist> <optioncol>
                   | <optioncol>

<optioncol> ::= DEFAULT <SQLSIMPLEEXPRESSION>                
              | NOT NULL
              | NULL
              | CONSTRAINT ID UNIQUE
              | UNIQUE
              | CONSTRAINT ID CHECK LEFT_PARENTHESIS <conditionColumn> RIGHT_PARENTHESIS
              | CHECK LEFT_PARENTHESIS <conditionColumn> RIGHT_PARENTHESIS
              | PRIMARY KEY
              | REFERENCES ID

<conditionColumn> ::= <conditioncheck>

<conditioncheck> ::= <SQLRELATIONALEXPRESSION>

<showstatement> ::= SHOW DATABASES SEMICOLON
                  | SHOW DATABASES LIKE <SQLNAME> SEMICOLON

<alterstatement> ::= ALTER <optionsalter> SEMICOLON

<optionsalter> ::= DATABASE <alterdatabase>
				 | TABLE <altertable>

<alterdatabase> ::= ID RENAME TO ID
				  | ID OWNER TO <typeowner>

<typeowner> ::= ID
              | CURRENT_USER
              | SESSION_USER

<altertable> ::= ID <alterlist>

<alterlist> ::= <alterlist> COMMA <typealter>
			  | <typealter>

<typealter> ::= ADD <addalter>
              | ALTER <alteralter>
              | DROP <dropalter>
              | RENAME  <renamealter>

<addalter> ::= COLUMN ID <typecol>
              | CHECK LEFT_PARENTHESIS <conditionColumn> RIGHT_PARENTHESIS
              | CONSTRAINT ID UNIQUE LEFT_PARENTHESIS ID RIGHT_PARENTHESIS
              | FOREIGN KEY LEFT_PARENTHESIS ID RIGHT_PARENTHESIS REFERENCES ID

<alteralter> ::= COLUMN ID SET NOT NULL
               | COLUMN ID TYPE <typecol>

<dropalter> ::= COLUMN ID
              | CONSTRAINT ID

<renamealter> ::= COLUMN ID TO ID

<dropstatement> ::= DROP <optionsdrop> SEMICOLON

<optionsdrop> ::= DATABASE <dropdatabase>
                | TABLE <droptable>

<dropdatabase> ::= IF EXISTS ID
                 | ID

<droptable> ::= ID

<DML> ::= <QUERYSTATEMENT>
        | <INSERTSTATEMENT>
        | <DELETESTATEMENT>
        | <UPDATESTATEMENT>

<UPDATESTATEMENT> ::= UPDATE ID <OPTIONS1> SET <SETLIST> <OPTIONSLIST2> SEMICOLON
                       | UPDATE ID SET <SETLIST> <OPTIONSLIST2> SEMICOLON
                       | UPDATE ID SET <SETLIST>  SEMICOLON 

<SETLIST> ::= <SETLIST> COMMA <COLUMNVALUES>
            | <COLUMNVALUES>

<COLUMNVALUES> ::= <OBJECTREFERENCE> EQUALS <SQLEXPRESSION2>

<SQLEXPRESSION2> ::= <SQLEXPRESSION2> PLUS <SQLEXPRESSION2> 
                   | <SQLEXPRESSION2> REST <SQLEXPRESSION2> 
                   | <SQLEXPRESSION2> DIVISION <SQLEXPRESSION2> 
                   | <SQLEXPRESSION2> ASTERISK <SQLEXPRESSION2> 
                   | <SQLEXPRESSION2> MODULAR <SQLEXPRESSION2>
                   | <SQLEXPRESSION2> EXPONENT <SQLEXPRESSION2> 
                   | REST <SQLEXPRESSION2> %prec UREST
                   | PLUS <SQLEXPRESSION2> %prec UPLUS
                   | LEFT_PARENTHESIS <SQLEXPRESSION2> RIGHT_PARENTHESIS
                   | ACOSD LEFT_PARENTHESIS <SQLEXPRESSION2> RIGHT_PARENTHESIS
                   | ASIND LEFT_PARENTHESIS <SQLEXPRESSION2> RIGHT_PARENTHESIS
                   | SUBSTRING LEFT_PARENTHESIS ID COMMA <SQLINTEGER> COMMA <SQLINTEGER> RIGHT_PARENTHESIS
                   | <SQLNAME>
                   | <SQLINTEGER>

<OPTIONSLIST2> ::= <WHERECLAUSE> <OPTIONS4>
                 | <WHERECLAUSE>
                 | <OPTIONS4>

<DELETESTATEMENT> ::= DELETE FROM ID <OPTIONSLIST> SEMICOLON
                    | DELETE FROM ID SEMICOLON

<OPTIONSLIST> ::= <OPTIONS1> <OPTIONS2> <WHERECLAUSE> <OPTIONS4>
                | <OPTIONS1> <OPTIONS2> <WHERECLAUSE>
                | <OPTIONS1> <WHERECLAUSE> <OPTIONS4>
                | <OPTIONS1> <OPTIONS2> <OPTIONS4>
                | <OPTIONS2> <WHERECLAUSE> <OPTIONS4>
                | <OPTIONS1> <OPTIONS2>
                | <OPTIONS1> <WHERECLAUSE>
                | <OPTIONS1> <OPTIONS4>
                | <OPTIONS2> <WHERECLAUSE>
                | <OPTIONS2> <OPTIONS4>
                | <WHERECLAUSE> <OPTIONS4>
                | <OPTIONS1>
                | <OPTIONS2>
                | <WHERECLAUSE>
                | <OPTIONS4>

<OPTIONS1> ::= ASTERISK <SQLALIAS>
             | ASTERISK
             | <SQLALIAS>

<OPTIONS2> ::= USING <USINGLIST>

<USINGLIST> ::= <USINGLIST> COMMA <SQLNAME>
              | <SQLNAME>

<OPTIONS4> : RETURNING <RETURNINGLIST>  

<EXPRESSIONRETURNING> ::= <EXPRESSIONRETURNING> COMMA <SQLEXPRESSION> <SQLALIAS>
                        | <SQLEXPRESSION> <SQLALIAS>

<INSERTSTATEMENT> ::= INSERT INTO <SQLNAME> LEFT_PARENTHESIS <LISTPARAMSINSERT> RIGHT_PARENTHESIS VALUES LEFT_PARENTHESIS <LISTVALUESINSERT> RIGHT_PARENTHESIS SEMICOLON
                    | INSERT INTO <SQLNAME> VALUES LEFT_PARENTHESIS <LISTVALUESINSERT> RIGHT_PARENTHESIS SEMICOLON

<LISTPARAMSINSERT> ::= <LISTPARAMSINSERT> COMMA <SQLNAME>
                     | <SQLNAME> 

<QUERYSTATEMENT> ::= <SELECTSTATEMENT> SEMICOLON

<SELECTSTATEMENT> ::= <SELECTWITHOUTORDER> <ORDERBYCLAUSE> <LIMITCLAUSE>
                    | <SELECTWITHOUTORDER> <ORDERBYCLAUSE> 
                    | <SELECTWITHOUTORDER> <LIMITCLAUSE> 
                    | <SELECTWITHOUTORDER>

<SELECTWITHOUTORDER> ::= <SELECTSET>
                       | <SELECTWITHOUTORDER> <TYPECOMBINEQUERY> ALL <SELECTSET>
                       | <SELECTWITHOUTORDER> <TYPECOMBINEQUERY> <SELECTSET>

<SELECTSET> ::= <SELECTQ> 
              | LEFT_PARENTHESIS <SUBQUERY> RIGHT_PARENTHESIS

<SELECTQ> ::= SELECT <SELECTLIST> <FROMCLAUSE>
            | SELECT <SELECTLIST> <FROMCLAUSE> <SELECTWHEREAGGREGATE>
            | SELECT <TYPESELECT> <SELECTLIST> <FROMCLAUSE>
            | SELECT <TYPESELECT> <SELECTLIST> <FROMCLAUSE> <SELECTWHEREAGGREGATE>
            | SELECT <SELECTLIST>

<SELECTLIST> ::= ASTERISK
               | <LISTITEM>

<LISTITEM> ::= <LISTITEM> COMMA <SELECTITEM>
             | <SELECTITEM>

<SELECTITEM> ::= <SQLEXPRESSION> <SQLALIAS>
               | <SQLEXPRESSION>
               | LEFT_PARENTHESIS <SUBQUERY> RIGHT_PARENTHESIS

<FROMCLAUSE> ::= FROM <FROMCLAUSELIST>

<FROMCLAUSELIST> ::= <FROMCLAUSELIST> COMMA <TABLEREFERENCE>
                   | <FROMCLAUSELIST> LEFT_PARENTHESIS <SUBQUERY> RIGHT_PARENTHESIS <SQLALIAS>
                   | <FROMCLAUSELIST> LEFT_PARENTHESIS <SUBQUERY> RIGHT_PARENTHESIS
                   | LEFT_PARENTHESIS <SUBQUERY> RIGHT_PARENTHESIS
                   | LEFT_PARENTHESIS <SUBQUERY> RIGHT_PARENTHESIS <SQLALIAS>
                   | <TABLEREFERENCE>

<SELECTWHEREAGGREGATE> ::= <WHERECLAUSE> <SELECTGROUPHAVING>
                         | <SELECTGROUPHAVING>
                         | <WHERECLAUSE>

<SELECTGROUPHAVING> ::= <GROUPBYCLAUSE>
                      | <HAVINGCLAUSE> <GROUPBYCLAUSE>
                      | <GROUPBYCLAUSE> <HAVINGCLAUSE>

<TABLEREFERENCE> ::= <SQLNAME> <SQLALIAS>
                   | <SQLNAME> <SQLALIAS> <JOINLIST>
                   | <SQLNAME> <JOINLIST>
                   | <SQLNAME>

<ORDERBYCLAUSE> ::= ORDER BY <ORDERBYEXPRESSION>

<ORDERBYEXPRESSION> ::= <LISTPARAMSINSERT> ASC
                      | <LISTPARAMSINSERT> DESC
                      | <LISTPARAMSINSERT>

<LIMITCLAUSE> ::= LIMIT <LIMITTYPES> OFFSET INT_NUMBER
                | LIMIT <LIMITTYPES>

<LIMITTYPES> ::= INT_NUMBER
               | ALL

<WHERECLAUSE> ::= WHERE <SQLEXPRESSION>

<GROUPBYCLAUSE> ::= GROUP BY <SQLEXPRESSIONLIST>

<HAVINGCLAUSE> ::= HAVING <SQLEXPRESSION>

<JOINLIST> ::= <JOINLIST> <JOINP>
             | <JOINP>

<JOINP> ::= <JOINTYPE> JOIN <TABLEREFERENCE> ON <SQLEXPRESSION>

<JOINTYPE> ::= INNER
             | LEFT OUTER
             | RIGHT OUTER
             | FULL OUTER

<SQLEXPRESSION> ::= <SQLEXPRESSION> OR <SQLEXPRESSION>
                  | <SQLEXPRESSION> AND <SQLEXPRESSION>
                  | NOT <EXISTSORSQLRELATIONALCLAUSE>
                  | <EXISTSORSQLRELATIONALCLAUSE>

<EXISTSORSQLRELATIONALCLAUSE> ::= <EXISTSCLAUSE>
                                | <SQLRELATIONALEXPRESSION>

<EXISTSCLAUSE> ::= EXISTS ID LEFT_PARENTHESIS <SUBQUERY> RIGHT_PARENTHESIS
                 | EXISTS LEFT_PARENTHESIS <SUBQUERY> RIGHT_PARENTHESIS

<SQLRELATIONALEXPRESSION> ::= <SQLSIMPLEEXPRESSION> <RELOP> <SQLSIMPLEEXPRESSION>
                            | <SQLSIMPLEEXPRESSION> <SQLINCLAUSE>
                            | <SQLSIMPLEEXPRESSION> <SQLBETWEENCLAUSE>
                            | <SQLSIMPLEEXPRESSION> <SQLLIKECLAUSE>
                            | <SQLSIMPLEEXPRESSION> <SQLISCLAUSE>
                            | <SQLSIMPLEEXPRESSION>

<SQLINCLAUSE> ::= NOT IN LEFT_PARENTHESIS <SUBQUERY> RIGHT_PARENTHESIS
                | NOT IN LEFT_PARENTHESIS <listain> RIGHT_PARENTHESIS
                | IN LEFT_PARENTHESIS <SUBQUERY> RIGHT_PARENTHESIS
                | IN LEFT_PARENTHESIS <listain> RIGHT_PARENTHESIS

<listain> ::= <listain> COMMA <SQLSIMPLEEXPRESSION>
            | <SQLSIMPLEEXPRESSION>

<SQLBETWEENCLAUSE> ::= NOT BETWEEN <SQLSIMPLEEXPRESSION> AND <SQLSIMPLEEXPRESSION>
                     | NOT BETWEEN SYMMETRIC <SQLSIMPLEEXPRESSION> AND <SQLSIMPLEEXPRESSION>
                     | BETWEEN <SQLSIMPLEEXPRESSION> AND <SQLSIMPLEEXPRESSION> 
                     | BETWEEN SYMMETRIC <SQLSIMPLEEXPRESSION> AND <SQLSIMPLEEXPRESSION>

<SQLLIKECLAUSE>  ::= NOT LIKE <SQLSIMPLEEXPRESSION>
                   | LIKE <SQLSIMPLEEXPRESSION>

<SQLISCLAUSE> ::= IS NULL
                | IS NOT NULL
                | ISNULL
                | NOTNULL
                | IS TRUE
                | IS NOT TRUE
                | IS FALSE
                | IS NOT FALSE
                | IS UNKNOWN
                | IS NOT UNKNOWN
                | IS NOT DISTINCT FROM <SQLNAME>
                | IS DISTINCT FROM <SQLNAME>

<SQLSIMPLEEXPRESSION> ::= <SQLSIMPLEEXPRESSION> PLUS <SQLSIMPLEEXPRESSION>
                        | <SQLSIMPLEEXPRESSION> REST <SQLSIMPLEEXPRESSION>
                        | <SQLSIMPLEEXPRESSION> ASTERISK <SQLSIMPLEEXPRESSION>
                        | <SQLSIMPLEEXPRESSION> DIVISION <SQLSIMPLEEXPRESSION>
                        | <SQLSIMPLEEXPRESSION> EXPONENT <SQLSIMPLEEXPRESSION>
                        | <SQLSIMPLEEXPRESSION> MODULAR <SQLSIMPLEEXPRESSION>
                        | REST <SQLSIMPLEEXPRESSION> %prec UREST
                        | PLUS <SQLSIMPLEEXPRESSION> %prec UPLUS
                        | <SQLSIMPLEEXPRESSION> BITWISE_SHIFT_RIGHT <SQLSIMPLEEXPRESSION>
                        | <SQLSIMPLEEXPRESSION> BITWISE_SHIFT_LEFT <SQLSIMPLEEXPRESSION>
                        | <SQLSIMPLEEXPRESSION> BITWISE_AND <SQLSIMPLEEXPRESSION>
                        | <SQLSIMPLEEXPRESSION> BITWISE_OR <SQLSIMPLEEXPRESSION>
                        | <SQLSIMPLEEXPRESSION> BITWISE_XOR <SQLSIMPLEEXPRESSION>
                        | BITWISE_NOT <SQLSIMPLEEXPRESSION> %prec UREST
                        | LEFT_PARENTHESIS <SQLEXPRESSION> RIGHT_PARENTHESIS
                        | <AGGREGATEFUNCTIONS>
                        | <GREATESTORLEAST>
                        | <EXPRESSIONSTIME>
                        | SQUARE_ROOT <SQLSIMPLEEXPRESSION>
                        | CUBE_ROOT <SQLSIMPLEEXPRESSION>
                        | <MATHEMATICALFUNCTIONS>
                        | <CASECLAUSE>
                        | <BINARY_STRING_FUNCTIONS>
                        | <TRIGONOMETRIC_FUNCTIONS>
                        | <SQLINTEGER>
                        | <OBJECTREFERENCE>
                        | NULL
                        | TRUE
                        | FALSE

<SQLEXPRESSIONLIST> ::= <SQLEXPRESSIONLIST> COMMA <SQLEXPRESSION>
                      | <SQLEXPRESSION>

<MATHEMATICALFUNCTIONS> ::= ABS LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                          | CBRT LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                          | CEIL LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                          | CEILING LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                          | DEGREES LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                          | DIV LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> COMMA <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                          | EXP LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                          | FACTORIAL LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                          | FLOOR LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                          | GCD LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> COMMA <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                          | LN LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                          | LOG LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                          | MOD LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> COMMA <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                          | PI LEFT_PARENTHESIS RIGHT_PARENTHESIS
                          | POWER LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> COMMA <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                          | RADIANS LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                          | ROUND LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> COMMA <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                          | SIGN LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                          | SQRT LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                          | WIDTH_BUCKET LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> COMMA <SQLSIMPLEEXPRESSION> COMMA <SQLSIMPLEEXPRESSION> COMMA <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                          | TRUNC LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                          | RANDOM LEFT_PARENTHESIS RIGHT_PARENTHESIS

<BINARY_STRING_FUNCTIONS> ::= LENGTH LEFT_PARENTHESIS <SQLNAME> RIGHT_PARENTHESIS
                            | SUBSTRING LEFT_PARENTHESIS <SQLNAME> COMMA <SQLINTEGER> COMMA <SQLINTEGER> RIGHT_PARENTHESIS
                            | TRIM LEFT_PARENTHESIS <SQLNAME> RIGHT_PARENTHESIS
                            | MD5 LEFT_PARENTHESIS <SQLNAME> RIGHT_PARENTHESIS
                            | SHA256 LEFT_PARENTHESIS <SQLNAME> RIGHT_PARENTHESIS
                            | SUBSTR LEFT_PARENTHESIS <SQLNAME> COMMA <SQLINTEGER> COMMA <SQLINTEGER> RIGHT_PARENTHESIS
                            | CONVERT LEFT_PARENTHESIS <SQLNAME> AS DATE RIGHT_PARENTHESIS
                            | CONVERT LEFT_PARENTHESIS <SQLNAME> AS INTEGER RIGHT_PARENTHESIS
                            | DECODE LEFT_PARENTHESIS <SQLNAME> COMMA <STRINGCONT> RIGHT_PARENTHESIS

<GREATESTORLEAST> ::= GREATEST LEFT_PARENTHESIS <LISTVALUESINSERT> RIGHT_PARENTHESIS
                    | LEAST LEFT_PARENTHESIS <LISTVALUESINSERT> RIGHT_PARENTHESIS

<CASECLAUSE> ::= CASE <CASECLAUSELIST> END ID
               | CASE <CASECLAUSELIST> ELSE <SQLSIMPLEEXPRESSION> END ID

<CASECLAUSELIST> ::= <CASECLAUSELIST> WHEN <SQLSIMPLEEXPRESSION> <RELOP> <SQLSIMPLEEXPRESSION> THEN <SQLSIMPLEEXPRESSION>
                   | <CASECLAUSELIST> WHEN <SQLSIMPLEEXPRESSION> THEN <SQLSIMPLEEXPRESSION>
                   | WHEN <SQLSIMPLEEXPRESSION> RELOP <SQLSIMPLEEXPRESSION> THEN <SQLSIMPLEEXPRESSION>
                   | WHEN <SQLSIMPLEEXPRESSION> THEN <SQLSIMPLEEXPRESSION>

<TRIGONOMETRIC_FUNCTIONS> ::= ACOS LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                            | ACOSD LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                            | ASIN LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                            | ASIND LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                            | ATAN LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                            | ATAND LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                            | ATAN2 LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> COMMA <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                            | ATAN2D LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> COMMA <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                            | COS LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                            | COSD LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                            | COT LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                            | COTD LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                            | SIN LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                            | SIND LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                            | TAN LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                            | TAND LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                            | COSH LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                            | SINH LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                            | TANH LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                            | ACOSH LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                            | ASINH LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS
                            | ATANH LEFT_PARENTHESIS <SQLSIMPLEEXPRESSION> RIGHT_PARENTHESIS

<SQLALIAS> ::= AS <SQLNAME>
             | <SQLNAME>

<EXPRESSIONSTIME> ::= EXTRACT LEFT_PARENTHESIS <DATETYPES> FROM TIMESTAMP <SQLNAME> RIGHT_PARENTHESIS
                    | NOW LEFT_PARENTHESIS RIGHT_PARENTHESIS
                    | DATE_PART LEFT_PARENTHESIS <SQLNAME> COMMA INTERVAL <SQLNAME> RIGHT_PARENTHESIS
                    | CURRENT_DATE
                    | CURRENT_TIME
                    | TIMESTAMP <SQLNAME>

<AGGREGATEFUNCTIONS> ::= <AGGREGATETYPES> LEFT_PARENTHESIS <CONTOFAGGREGATE> RIGHT_PARENTHESIS
                       | <AGGREGATETYPES> LEFT_PARENTHESIS <CONTOFAGGREGATE> RIGHT_PARENTHESIS <SQLALIAS>

<CONTOFAGGREGATE> ::= ASTERISK
                    | <SQLSIMPLEEXPRESSION>

<OBJECTREFERENCE> ::= <SQLNAME> DOT ASTERISK
                    | <SQLNAME>

<LISTVALUESINSERT> ::= <LISTVALUESINSERT> COMMA <SQLSIMPLEEXPRESSION>
                     | <SQLSIMPLEEXPRESSION>

<TYPECOMBINEQUERY> ::= UNION
                     | INTERSECT
                     | EXCEPT

<RELOP> ::= EQUALS 
          | NOT_EQUAL
          | GREATE_EQUAL
          | GREATE_THAN
          | LESS_THAN
          | LESS_EQUAL
          | NOT_EQUAL_LR

<AGGREGATETYPES> ::= AVG
                   | SUM
                   | COUNT
                   | MAX
                   | MIN

<SQLINTEGER> ::= INT_NUMBER
               | FLOAT_NUMBER

<SQLNAME> ::= STRINGCONT
            | CHARCONT
            | ID

<TYPESELECT> ::= ALL
               | DISTINCT
               | UNIQUE

<SUBQUERY> ::= SELECTSTATEMENT


<INDEXES_STATEMENT> ::= <CREATE_INDEXES>
                      | <DROP_INDEXES> SEMICOLON
                      | <ALTER_INDEXES> SEMICOLON


<DROP_INDEXES> ::= DROP INDEX CONCURRENTLY IF EXISTS <columnlist> CASCADE
                |  DROP INDEX CONCURRENTLY IF EXISTS <columnlist> RESTRICT
                |  DROP INDEX IF EXISTS <columnlist> RESTRICT
                |  DROP INDEX IF EXISTS <columnlist> CASCADE
                |  DROP INDEX <columnlist> CASCADE
                |  DROP INDEX <columnlist> RESTRICT 
                |  DROP INDEX CONCURRENTLY IF EXISTS <columnlist>
                |  DROP INDEX CONCURRENTLY <columnlist>
                |  DROP INDEX IF EXISTS <columnlist>
                |  DROP INDEX <columnlist>


<ALTER_INDEXES> ::= ALTER INDEX IF EXISTS ID RENAME TO ID
                  | ALTER INDEX ID RENAME TO ID


<CREATE_INDEXES> ::= CREATE <TYPE_INDEX> ID ON ID <OPTIONS1_INDEXES> LEFT_PARENTHESIS <BODY_INDEX> RIGHT_PARENTHESIS <WHERECLAUSE> SEMICOLON
                   | CREATE <TYPE_INDEX> ID ON ID <OPTIONS1_INDEXES> LEFT_PARENTHESIS <BODY_INDEX> RIGHT_PARENTHESIS  SEMICOLON
                   | CREATE <TYPE_INDEX> ID ON ID LEFT_PARENTHESIS <BODY_INDEX> RIGHT_PARENTHESIS  <WHERECLAUSE> SEMICOLON
                   | CREATE <TYPE_INDEX> ID ON ID LEFT_PARENTHESIS <BODY_INDEX> RIGHT_PARENTHESIS SEMICOLON


<TYPE_INDEX> ::= INDEX
               | UNIQUE INDEX

<OPTIONS1_INDEXES> ::= USING <TYPE_MODE_INDEX>

<TYPE_MODE_INDEX> ::= BTREE 
                    | HASH

<BODY_INDEX> ::=  <BODY_INDEX> COMMA LOWER LEFT_PARENTHESIS ID RIGHT_PARENTHESIS <OPTIONS2_INDEXES>
               |  <BODY_INDEX> COMMA ID <OPTIONS2_INDEXES>
               |  <BODY_INDEX> COMMA LOWER LEFT_PARENTHESIS ID RIGHT_PARENTHESIS
               |  <BODY_INDEX> COMMA ID 
               |  <ID OPTIONS2_INDEXES>
               |  LOWER LEFT_PARENTHESIS ID RIGHT_PARENTHESIS
               |  LOWER LEFT_PARENTHESIS ID RIGHT_PARENTHESIS <OPTIONS2_INDEXES>
               |  ID

<OPTIONS2_INDEXES> ::= ASC NULLS FIRST 
                     | DESC NULLS LAST
                     | NULLS FIRST
                     | NULLS LAST
                     | ASC
                     | DESC


<CALL_FUNCTIONS_PROCEDURE> ::= ID LEFT_PARENTHESIS <LISTVALUESINSERT>  RIGHT_PARENTHESIS
                             | ID LEFT_PARENTHESIS  RIGHT_PARENTHESIS 
                             | EXECUTE ID LEFT_PARENTHESIS  RIGHT_PARENTHESIS 
                             | EXECUTE ID LEFT_PARENTHESIS <LISTVALUESINSERT>  RIGHT_PARENTHESIS




<SQL_FUNCTIONS> ::= CREATE FUNCTION ID LEFT_PARENTHESIS <LIST_ARGUMENT> RIGHT_PARENTHESIS RETURNS <TYPERETURNS> AS <BODYBLOCK>    LANGUAGE PLPSQL SEMICOLON 
                | CREATE FUNCTION ID LEFT_PARENTHESIS RIGHT_PARENTEHSIS RETURNS <TUPERETURNS> AS <BODYBLOCK> LANGUAGE PLPGSPL SEMICOLON
                | CREATE FUNCTION ID LEFT_PARENTHESIS <LIST_ARGUMENT> RIGHT_PARENTEHSIS AS <BODYBLOCKK> LANGUAGE PLPGSQL SEMICOLON
                | CREATE FUNCTION ID LEFT_PARENTHESIS RIGHT_PARENTHESIS AS <BODYBLOCK> LANGUAGE PLPGSQL SEMICOLON

<SQL_DROP_FUNCTION> ::= DROP FUNCTION IF EXISTS <DETAIL_FUNC_DROP> SEMICOLON
                    | DROP FUNCTION <DETAIL_FUNC_DROP> SEMICOLON

<SQL_DROP_PROCEDURE> ::= DROP PROCEDURE IF EXISTS <DETAIL_FUNC_DROP> SEMICOLON
                     | DROP PROCEDURE <DETAIL_FUNC_DROP> SEMICOLON

<DETAIL_FUNC_DROP> ::= <DETAIL_FUNC_DROP> COMMA <FUNCTIONS_TO_DROP>
                     | <FUNCTIONS_TO_DROP>

<FUNCTIONS_TO_DROP> ::= ID LEFT_PARENTHESIS <LIST_ARGUMENT> RIGHT_PARENTHESIS
                      | ID LEFT_PARENTHESIS RIGHT_PARENTHESIS
                      | ID

<SQL_PROCEDURES> ::= CREATE PROCEDURE ID LEFT_PARENTHSIS <LIST_ARGUMENT> RIGHT_PARENTHESIS LANGUAGE PLPGSQL AS <BODYBLOCK>
                   | CREATE PROCEDURE ID LEFT_PARENTHESIS RIGHT_PARENTHESIS LANGUAGE PLPGSQL AS <BODYBLOCK>

<TYPERETURNS> ::= <TYPECOL>
                | VOID
                | TABLE LEFT_PARENTEHSIS <LIST_ARGUMENT> RIGHT_PARENTHESIS

<LIST_ARGUMENT> ::= <LIST_ARGUMENT> COMMA <PARAM>
                  | <PARAM>

<PARAM> ::= ID <TYPECOL>
          | <TYPECOL>
          | VARIADIC ID <TYPECOL>
          | ID ID

<BODYBLOCK> ::= DOUBLE_DOLLAR <BODY_DECLARATION> DOUBLE_DOLLAR
             |  DOLLAR <SQLNAME> DOLLAR <BODY_DECLARATION> DOLLAR <SQLNAME> DOLLAR

<BODY_DECLARATION> ::= <HEADERBODYLIST> BEGIN <STATEMENTS> END ID SEMICOLON
                    |  <HEADERBODYLIST> BEGIN <STATEMENTS> EXCEPTION <BODYEXCEPTIONLIST> END ID SEMICOLON
                    |  <HEADERBODYLIST> BEGIN <STATEMENTS> END SEMICOLON
                    |  <HEADERBODYLIST> BEGIN <STATEMENTS> EXCEPTION <BODYEXCEPTIONLIST> END SEMICOLON
                    |   BEGIN <STATEMENTS> END ID SEMICOLON
                    |   BEGIN <STATEMENTS> EXCEPTION <BODYEXCEPTIONLIST> END ID SEMICOLON
                    |   BEGIN <STATEMENTS> END SEMICOLON
                    |   BEGIN <STATEMENTS> EXCEPTION <BODYEXCEPTIONLIST> END SEMICOLON

<HEADERBODYLIST> ::= <HEADERBODYLIST> <HEADER>
                   | <HEADER>

<HEADER> ::= BITWISE_SHIFT_LEFT ID BITWISE_SHIFT_RIGHT
           | DECLARE <DECLARATIONSLIST>

<DECLARATIONSLIST> ::= <DECLARATIONSLIST> <SQL_VAR_DECLARATIONS>
                    |  <SQL_VAR_DECLARATIONS>

<SQL_VAR_DECLARATIONS> ::= ID CONSTANT <TYPEDECLARE> <DETAILDECLARATION> SEMICOLON
                        |  ID CONSTANT <TYPEDECLARE> SEMICOLON
                        |  ID <TYPEDECLARE> <DETAILDECLARATION> SEMICOLON
                        |  ID <TYPEDECLARE> SEMICOLON
                        |  ID ALIAS FOR DOLLAR <SQLINTEGER> SEMICOLON 


<TYPEDECLARE> ::= <TYPECOL>
                |  ID MODULAR ROWTYPE
                |  ID DOT ID MODULAR TYPE
                |  RECORD
                |  OUT

<DETAILDECLARATION> ::= COLLATE ID NOT NULL <ASSIGNATION_SYMBOL> <PLPSQL_EXPRESSION>
                     |  NOT NULL <ASSIGNATION_SYMBOL> <PLPSQL_EXPRESSION>
                     |  COLLATE ID NOT NULL
                     |  COLLATE ID <ASSIGNATION_SYMBOL> <PLPSQL_EXPRESSION>
                     |  COLLATE ID
                     |  NOT NULL
                     |  <ASSIGNATION_SYMBOL> <PLPSQL_EXPRESSION>

<ASSIGNATION_SYMBOL> ::= EQUALS
                       | COLONEQUALS
                       | DEFAULT

<STATEMENTS> ::= <OPTIONS_STATEMENTS> RETURN <PLPSQL_EXPRESSION> SEMICOLON
               | <OPTIONS_STATEMENTS> RETURN SEMICOLON
               | <RETURN> SEMICOLON
               | <OPTIONS_STATEMENTS>

<OPTIONS_STATEMENTS> ::= <OPTIONS_STATEMENTS> <STATEMENTTYPE>
                     | <STATEMENTTYPE>

<STATEMENTTYPE> ::= <PLPSQL_EXPRESSION> SEMICOLON
                  | <PLPSQL_PRIMARY_EXPRESSION> <ASSIGNATION_SYMBOL> <QUERY_STATEMENT>
                  | <PLPSQL_PRIMARY_EXPRESSION> <ASSIGNATION_SYMBOL> LEFT_PARENTHESIS <INSERTSTATEMENT> RIGTH_PARENTHESIS
                  | <PLPSQL_PRIMARY_EXPRESSION> <ASSIGNATION_SYMBOL> <INSERTSTATEMENT>
                  | <PLPSQL_PRIMARY_EXPRESSION> <ASSIGNATION_SYMBOL> LEFT_PARENTHESIS <DELETESTATEMENT> RIGTH_PARENTHESIS
                  | <PLPSQL_PRIMARY_EXPRESSION> <ASSIGNATION_SYMBOL> <DELETESTATEMENT>
                  | <PLPSQL_PRIMARY_EXPRESSION> <ASSIGNATION_SYMBOL> LEFT_PARENTHESIS <UPDATESTATEMENT> RIGTH_PARENTHESIS
                  | <PLPSQL_PRIMARY_EXPRESSION> <ASSIGNATION_SYMBOL> <UPDATESTATEMENT>
                  | <RAISE_EXCEPTION>
                  | <BODY_DECLARATION>
                  | <IFSTATEMENT>
                  | <CASECLAUSE>
                  | <DML>
                  | <CALL_FUNCTIONS_PROCEDURE> SEMICOLON

<PLPSQL_EXPRESSION> ::= <PLPSQL_EXPRESSION> CONCAT <PLPSQL_EXPRESSION>
                      | <PLPSQL_EXPRESSION> AND <PLPSQL_EXPRESSION>
                      | <PLPSQL_EXPRESSION> OR <PLPSQL_EXPRESSION>
                      | <PLPSQL_PRIMARY_EXPRESSION> <ASSIGNATION_SYMBOL> <SQLRELATIONALEXPRESSION>
                      | <PLPSQL_PRIMARY_EXPRESSION> <ASSIGNATION_SYMBOL> <CALL_FUNCTIONS_PROCEDURE>
                      | <PLPSQL_PRIMARY_EXPRESSION> NOT_EQUAL <PLPSQL_PRIMARY_EXPRESSION>
                      | <PLPSQL_PRIMARY_EXPRESSION> GREATE_EQUAL <PLPSQL_PRIMARY_EXPRESSION>
                      | <PLPSQL_PRIMARY_EXPRESSION> GREATE_THAN <PLPSQL_PRIMARY_EXPRESSION>
                      | <PLPSQL_PRIMARY_EXPRESSION> LESS_THAN <PLPSQL_PRIMARY_EXPRESSION>
                      | <PLPSQL_PRIMARY_EXPRESSION> LESS_EQUAL <PLPSQL_PRIMARY_EXPRESSION>
                      | <PLPSQL_PRIMARY_EXPRESSION>


<PLPSQL_PRIMARY_EXPRESSION> ::= <PLPSQL_PRIMARY_EXPRESSION> PLUS <PLPSQL_PRIMARY_EXPRESSION>
                              | <PLPSQL_PRIMARY_EXPRESSION> REST <PLPSQL_PRIMARY_EXPRESSION>
                              | <PLPSQL_PRIMARY_EXPRESSION> ASTERISK <PLPSQL_PRIMARY_EXPRESSION>
                              | <PLPSQL_PRIMARY_EXPRESSION> DIVISION <PLPSQL_PRIMARY_EXPRESSION>
                              | <PLPSQL_PRIMARY_EXPRESSION> EXPONENT <PLPSQL_PRIMARY_EXPRESSION>
                              | <PLPSQL_PRIMARY_EXPRESSION> MODULAR <PLPSQL_PRIMARY_EXPRESSION>
                              | <LEFT_PARENTHESIS> <PLPSQL_EXPRESSION> <RIGHT_PARENTHESIS>
                              |  REST <PLPSQL_PRIMARY_EXPRESSION> %prec UREST
                              |  PLUS <PLPSQL_PRIMARY_EXPRESSION> %prec UPLUS
                              | <AGGREGATEFUNCTIONS>
                              | <GREATESTORLEAST>
                              | <EXPRESSIONSTIME>
                              |  SQUARE_ROOT <SQLSIMPLEEXPRESSION>
                              |  CUBE_ROOT <SQLSIMPLEEXPRESSION>
                              | <MATHEMATICALFUNCTIONS>
                              | <BINARY_STRING_FUNCTIONS>
                              | <TRIGONOMETRIC_FUNCTIONS>
                              |  TRUE
                              |  FALSE
                              | <OBJECTREFERENCE>
                              | <SQLINTEGER>
                              |  DOLLAR <SQLINTEGER>
    

<ifStatement> ::= IF <SQLEXPRESSION> THEN <STATEMENTS> <elseIfBlocks> ELSE <STATEMENTS> END IF SEMICOLON
                | IF <SQLEXPRESSION> THEN <STATEMENTS> <elseIfBlocks> END IF SEMICOLON
                | IF <SQLEXPRESSION> THEN <STATEMENTS> ELSE <STATEMENTS> END IF SEMICOLON
                | IF <SQLEXPRESSION> THEN <STATEMENTS> END IF SEMICOLON


<elseIfBlocks> ::=  <elseIfBlocks> <elseIfBlock>
                 | <elseIfBlock>

<elseIfBlock> ::= <elseIfWord> <SQLEXPRESSION> THEN <STATEMENTS>

<elseIfWord> ::= ELSEIF
               | ELSIF

<bodyExceptionList> ::= <bodyExceptionList> <bodyException>
                      | <bodyException>

<bodyException> ::= WHEN <SQLEXPRESSION> THEN <STATEMENTS>

<RAISE_EXCEPTION> ::= RAISE NOTICE <SQLNAME> COMMA <OBJECTREFERENCE> SEMICOLON
                   | RAISE <SQLNAME> COMMA <OBJECTREFERENCE> SEMICOLON
```