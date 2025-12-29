
## Instructions for PAC-USWHS002-WF-2 compatible module

A reminder of the module:
<html><table><tr>
  <td><img src="/images/WF-2/WF-2-Label.png" height="640" alt="Label View"></td>
  <td><img src="/images/WF-2/WF-2-Front.png" height="640" alt="Front View"></td>
  <td><img src="/images/WF-2/WF-2-Top.png"   height="640" alt="Top View"></td>
</tr></table></html>  

Remember the CN105 wire harness provided with the WF-2 is not compatible with the connector on the WF-1 without an adapter cable.  Please ensure you select the correct version of this project to ensure connector compatibility.

## Fabrication
PCB Manufacturing can be accomplished using whichever fabricator you wish.  For convenience, a [PCBWay](https://www.pcbway.com/project/shareproject/Mitsubishi_ESPHome_CN105_WF-2-Compatible.html) 
project has been created that makes creating the PCB basically one click using PCBWay as the fabricator.   This option allows you to either create PCBs that you assemble using the parts below, or have the boards fully assembled so you just program and plugin.  You can also allow download of all gerber files, etc. in case you want to use a different vendor. 

A copy of all files also exists here: [Gerber files](/pcb_assembly/WF-2/gerber).  These should be identical to the ones at PCBWay - they are insurance in case
something happens to the PCBWay community site.  If you notice any discrepancy please let me know.

The supplied gerber files should be portable to any manufacturer not just PCBWay.

Version History
- V1.0 - 06/01/2025 - Initial Version
- V1.1 - 07/12/2025 - Fix issue in which i2c connector is reversed
- V1.2 - 12/09/2025 - Fix issue in which SDA/SDL need to be pulled high NOT low
- V1.3 - 12/27/2025 - Fork of WF-1 board to change connector to JST PA 2.0mm spacing

Please ensure you are using the latest version of the gerber files.

### Parts lists
|Qty|Part Desc.|Link|
|--|--|--|
| 1 | CN105 Connector | [S05B-PASK-2](https://www.digikey.com/en/products/detail/jst-sales-america-inc/S05B-PASK-2/926756) |
| 1 | I2C/Stemma | [S4B-PH-K-S](https://www.digikey.com/en/products/detail/jst-sales-america-inc/S4B-PH-K-S/926628) |
| 1 | Wavemaker ESP32-C6-Zero | [ESP32-C6-Zero-M](https://www.amazon.com/dp/B0D1K19W2Y?ref_=ppx_hzsearch_conn_dt_b_fed_asin_title_1) |
| 1 | 1A 32V Fuse | [MFU0805FF01000P500](https://www.digikey.com/en/products/detail/vishay-beyschlag-draloric-bc-components/MFU0805FF01000P500/1202619) |
| 6 | RES 10K OHM 1% 1/8W | [CRGCQ0805F10K](https://www.digikey.com/en/products/detail/te-connectivity-passive-product/CRGCQ0805F10K/8576363) |
| 2 | MOSFET N-CH 50V 220MA | [BSS138](https://www.digikey.com/en/products/detail/onsemi/BSS138/244210) |

The resulting assembled PCB should look like the following:

![WF-2 Assembled](/images/WF-2/WF-2-PCB-V1.3.png)

## Case
To complete the project I created a 3D printed case that is as close to the same dimensions as the original PAC wifi module.  It is a tooless design that simply snaps together (it does require a small screwdriver or really strong fingernails to disassemble).  

![PCB in Case](/images/Case-compare-front.png)

The case was printed using white PLA using quality settings (0.2mm, 15% infill, no supports, etc.).  While there is a bit of play in the PCB restraint system, I did aim for precision to have the top/bottom snap to fit, etc.    You can find the STL files for the top & bottom of the case in the [3d_case](/pcb_assembly/WF-2/3d_case) directory.  If there is sufficient interest I can place them on printables.

## Final Notes

This project could be done with larger components, there is sufficient space.  However I wanted the opportunity to learn surface mount components and chose 805 size as a compromise.  It would also enable installation of some or all of the components at fabrication time if that was ever interesting to someone.
