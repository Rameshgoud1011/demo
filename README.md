# demo
This is my first repository 
1. CREATE A TABLE TO REPRESENT SB-ACCOUNT OF A BANK CONSISTING OF ACCOUNT-NO, CUSTOMER-NAME, BALANCE-AMOUNT.
WRITE A PL/SQL BLOCK TO IMPLEMENT DEPOSIT AND WITHDRAW. WITHDRAWS SHOULD  NOT BE ALLOWED IF THE BALANCE GOES BELOW RS.1000.

CREATE table sb_acc(AC_NO number(11),C_NAME varchar2(30),BAL number, PRIMARY KEY(ac_no));

INSERT into sb_acc VALUES('&ac_no','&c_name','&balance');

PL/SQL block
DECLARE
acno SB_ACC.ac_no%type:='&acno';
amt SB_ACC.bal%type:='&amount';
balance SB_ACC.bal%type;
ch char:='&Transaction';      --D:Deposit   W:Withdraw
BEGIN
SELECT bal into balance from SB_ACC WHERE ac_no=acno;
ch:=UPPER(ch);
CASE
WHEN ch='D' then
balance:=balance+amt;
dbms_output.put_line('TRANSACTION SUCCESSFULLY COMPLETED');
dbms_output.put_line('YOUR CURRENT BALANCE : '||balance);

WHEN ch='W' then
if(balance>1000) then
balance:=balance-amt;
dbms_output.put_line('TRANSACTION SUCCESSFULLY COMPLETED');
dbms_output.put_line('YOUR CURRENT BALANCE : '||balance);
else
dbms_output.put_line('AMOUNT NOT AVAILABLE');
end if;
ELSE
dbms_output.put_line('WRONG CHOICE');
END CASE;

UPDATE SB_ACC set bal=balance WHERE ac_no=acno;

COMMIT;
END;
/
