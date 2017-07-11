This is a python script which creates the framework for various analog blocks.

Will create blank file templates and directory structures for a given type of block, following a naming convention.

Can hook into SKILL scripts to actually generate placeholders for the blocks including symbols.
Should be extended to hook into IFACE for defining mixed-signal systems
Can also be used to define top level test bench standards.

Example: asking this program to generate an OpAmp would produce the following files:
	You would need to provide certain inputs -
		pin IO list
		block spec table

LIBRARY BLOCKS:

* LIB/block_name/schematic.oa
* LIB/block_name/symbol
LIB/block_name/schematic_behavioral.vams

SIMULATION BLOCKS:

* SIM/tb_block_name/schematic
	test bench schematic would auto-inflate with proper stimulus, side-by-side behavioral comparison,
		uses generic TB architecture. proper irun files. etc etc.
* SIM/tb_block_name/config
* SIM/tb_block_name/adexl
	adexl view with all required "opamp" sims, corners, and measurements already set up
		ANALYSES:
		STB CM		AC - OL		AC-PSRR		AC-CMRR	
		STB DM		tran-step	DCMatch
		
		CORNERS:
		W.C. one-hot	VCC/VREG	Temp		M.C. Mismatch	
	
		MEASUREMENTS:
		CMRR	PSRR	DC Gain		Linearity	Step Response (tpd, tr, os%)
		PM	GM	VsatL/H		ICC		Load
		Offset	Drift	device sat.	BW
		

SIMULINK MODEL FILES:
create files for behavioral level modeling, if it makes sense for the block

* MIX/block_name/block_name.slx
* MIX/tb/tb_block_name.slx

DOCUMENTATION/REPORTING:
create HTML template for the following pages and fill in with what is known.

* DOC/block_name/IOtable
* DOC/block_name/spec_table
* DOC/block_name/sim_results/[PM/GM/DCGain/Vsat/ICC/Lin etc]
* DOC/block_name/datasheet_specs_affected
			linked list of all datasheet specs affected by this block
