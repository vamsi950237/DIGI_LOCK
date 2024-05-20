# DIGI_LOCK
# It is required to implement a digital lock that will accept a specific bit sequence  “101100” through an input button “b_in” serially in synchronism with the negative edge of an input clock, and will generate an “unlock” signal “1” as output; for any other bit sequence the “unlock” signal will remain at logic “0”.  An active low “clear” signal is used to asynchronously reset the lock in its initial/default state.

# Write a Verilog module to implement the specification as Moore machine using the following template:
#    module dlock (unlock, b_in, clear, clk);
![image](https://github.com/RESMIRNAIR/DIGI_LOCK/assets/154305926/61af2bd3-8217-461d-bbce-df66969fe413)
### Program:
~~~
module dlock (unlock, b_in, clear, clk);
   input b_in, clear, clk;
   output reg unlock;
   reg [2:0] state; // The machine states 
   parameter S0=3'b000, S1=3'b001, S2=3'b010, S3=3'b011,     S4=3'b100, S5=3'b101, S6=3'b110, S7=3'b111; 
always @(negedge clk or clear) begin
        if (clear == 0) state <= S0;
        else case (state)
             S0: state <= b_in ? S1 : S7;
 	        S1: state <= b_in ? S7 : S2;
	        S2: state <= b_in ? S3 : S7;
 	        S3: state <= b_in ? S4 : S7;
	        S4: state <= b_in ? S7 : S5;
	        S5: state <= b_in ? S7 : S6;
	        S6: state <= S6;
	        S7: state <= S7;
              default: state <= S0;
        endcase
   end
always @(state) 
  begin  
      case (state)
            S0, S1, S2, S3, S4, S5, S7: unlock = 0;
            S6: unlock = 1;
      endcase
   end
endmodule
~~~
### Output
![Screenshot 2024-05-20 085214](https://github.com/Shaiksushma123/DIGI_LOCK/assets/159005642/4c667817-fe44-4577-bd79-75b4dd8f36b3)
