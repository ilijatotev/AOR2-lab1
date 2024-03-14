library IEEE;
use IEEE.std_logic_1164.all;

entity muX is
port(
	a: in std_logic_vector(3 downto 0);
	sel: in std_logic_vector (1 downto 0);
    c: out std_logic);
end muX;

architecture muX_arch of muX is
begin
	stimuli: process(a,sel)
    begin
    	if (sel="00") then
        c<=a(0);
        elsif (sel="01") then
        c<=a(1);
        elsif (sel="10") then
        c<=a(2);
        else
        c<=a(3);
        end if;
	end process;
end architecture;



--TESTBENCH
library IEEE;
use IEEE.std_logic_1164.all;

entity testbench is
end testbench;

architecture tb of testbench is

component muX is
port(
	a:in std_logic_vector(3 downto 0);
	sel:in std_logic_vector(1 downto 0);
    c:out std_logic);
end component;
signal a_in: std_logic_vector(3 downto 0);
signal c_out: std_logic;
signal sel_in: std_logic_vector (1 downto 0);

begin
uut: muX port map(a=>a_in, sel=>sel_in, c=>c_out);
process
begin
a_in<="1000";
sel_in<="00";
wait for 10ns;


a_in<="1000";
sel_in<="01";
wait for 10ns;


a_in<="1000";
sel_in<="10";
wait for 10ns;


a_in<="1000";
sel_in<="11";
wait for 10ns;


end process;
end architecture;