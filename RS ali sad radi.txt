library IEEE;
use IEEE.std_logic_1164.all;


entity rsff is
port(R,S,clk:in std_logic;
    Q:out std_logic);
end entity;

architecture rsff_arch of rsff is
begin
state_change: process(clk)
begin
	if clk'event and clk='1' then
    	if (R='1' and S='0') then
        	Q<='0';
        elsif (R='0' and S='1') then
        	Q<='1';
        elsif (R='0' and S='0') then
        	Q<=Q;
        else
        	Q<='Z';
        end if;
    end if;
end process;
end architecture;


--TESTBENCH

library IEEE;
use IEEE.std_logic_1164.all;

entity testbench is
end entity;

architecture tb of testbench is
signal Q,R,S,clk:std_logic;
begin
uut: entity work.rsff
port map(Q=>Q,R=>R,S=>S,clk=>clk);
clock: process
begin
clk<='1';
wait for 5ns;
clk<='0';
wait for 5ns;
clk<='1';
wait for 5ns;
clk<='0';
wait for 5ns;
end process clock;

rad: process
begin

wait for 10ns;
wait for 10ns;

R <= '0'; S <= '0'; wait for 10 ns;
R <= '0'; S <= '1'; wait for 10 ns;

R <= '0'; S <= '0'; wait for 10 ns;

R <= '1'; S <= '0'; wait for 10 ns;
R <= '1'; S <= '1'; wait for 10 ns;


end process rad;
end architecture;