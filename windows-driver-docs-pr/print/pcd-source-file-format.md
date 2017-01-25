---
title: PCD Source File Format
author: windows-driver-content
description: PCD Source File Format
MS-HAID:
- 'plotter\_a4eba66a-0479-4fa5-a32c-d1a0ad009eed.xml'
- 'print.pcd\_source\_file\_format'
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: 8651d6ca-7cd7-4c07-aa66-2766dd2222e0
keywords: ["Plotter Driver WDK print , minidrivers", "MSPlot WDK print , minidrivers", "minidrivers WDK MSPlot", "PCD files WDK MSPlot", ".pcd files", "keywords WDK MSPlot"]
---

# PCD Source File Format


## <a href="" id="ddk-pcd-source-file-format-gg"></a>


All plotter device characteristics are specified using the following format:

*keyword* { *value* }

where *keyword* is one of the PCD source file keywords and *value* is a quoted string or numeric value. For example, the following statement specifies that the plotter supports color:

```
ColorCap {1}
```

Keywords are described in the following table.

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Keyword</th>
<th>Value Definition</th>
<th>Default Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>BezierCap</strong></p></td>
<td><p>1=Device supports HPGL2 Beziers extension.</p>
<p>0=No support.</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>ColorCap</strong></p></td>
<td><p>1=Color device</p>
<p>0=Monochrome device</p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>COLORINFO</strong></p></td>
<td><p>Thirty DWORD-sized values representing the contents of a [<strong>COLORINFO</strong>](https://msdn.microsoft.com/library/windows/hardware/ff539441) structure.</p></td>
<td><p></p>
{
{6810,3050,0}, // xr, yr, Yr
{2260,6550,0}, // xg, yg, Yg
{1810,500,0}, // xb, yb, Yb
{2000,2450,0}, // xc, yc, Yc
{5210,2100,0}, // xm, ym, Ym
{4750,5100,0}, // xy, yy, Yy
{3324,3474,10000}, // xw, yw, Yw
10000,10000,10000, // RGB gamma
1422,952, // M/C, Y/C
787,495, // C/M, Y/M
324,248 // C/Y, M/Y
}</td>
</tr>
<tr class="even">
<td><p><strong>DeviceMargin</strong></p></td>
<td><p>Four DWORD-sized values representing the left, top, right, and bottom paper margins, in 1/1000 mm units.</p></td>
<td><p></p>
{5000,
5000,
5000,
36000}</td>
</tr>
<tr class="odd">
<td><p><strong>DeviceName</strong></p></td>
<td><p>Quoted string representing a displayable device name (31 characters max.)</p></td>
<td><p>&quot;HPGL/2 Plotter&quot;</p></td>
</tr>
<tr class="even">
<td><p><strong>DevicePelsDPI</strong></p></td>
<td><p>One DWORD-sized value representing the device's effective DPI. For more information see the <strong>upDevicePelsDPI</strong> member of [<strong>GDIINFO</strong>](https://msdn.microsoft.com/library/windows/hardware/ff566484).</p></td>
<td><p>The default is zero, causing GDI to calculate a value.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceSize</strong></p></td>
<td><p>Two DWORD-sized values representing maximum paper size, in <em>x</em> and <em>y</em> coordinates of 1/1000 mm units.</p>
<p>A <em>y</em> value of 25400 (1 inch) or less indicates the device accepts variable paper lengths.</p></td>
<td><p></p>
{215900,
279400}</td>
</tr>
<tr class="even">
<td><p><strong>FormInfo</strong></p></td>
<td><p>A form description for each form supported by the plotter. For more information, see the <strong>Form Descriptions</strong> section that follows this Table.</p></td>
<td><p>None.</p></td>
</tr>
<tr class="odd">
<td><p><strong>HTPatternSize</strong></p></td>
<td><p>One of the HT_PATSIZE_-prefixed constants that identify standard halftoning patterns.</p></td>
<td><p>0xffffffff</p></td>
</tr>
<tr class="even">
<td><p><strong>InitString</strong></p></td>
<td><p>Quoted C-language string representing commands sent to the printer by the driver's [<strong>DrvStartPage</strong>](https://msdn.microsoft.com/library/windows/hardware/ff556298) function.</p></td>
<td><p>NULL string.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxCopies</strong></p></td>
<td><p>Maximum number of copies per page that the device can render.</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p><strong>MaxPens</strong></p></td>
<td><p>Number of pens (32 max.)</p></td>
<td><p>8</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxPolygonPts</strong></p></td>
<td><p>Maximum number of points to define a polygon to be stroked or filled.</p></td>
<td><p>128</p></td>
</tr>
<tr class="even">
<td><p><strong>MaxQuality</strong></p></td>
<td><p>Number of quality levels (4 max.)</p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxScale</strong></p></td>
<td><p>Maximum scale size. 0-10000 (100 is 100%)</p></td>
<td><p>100</p></td>
</tr>
<tr class="even">
<td><p><strong>NoBitmapFont</strong></p></td>
<td><p>1=Device does not support bitmap fonts.</p>
<p>0=Bitmap fonts are supported.</p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>PaperTrayCap</strong></p></td>
<td><p>1=Device has paper tray source.</p>
<p>0=No support.</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>PaperTraySize</strong></p></td>
<td><p>Two DWORD-sized values representing the paper tray width and height, in 1/1000 mm units.</p></td>
<td><p></p>
{-1,
-1}</td>
</tr>
<tr class="odd">
<td><p><strong>PlotDPI</strong></p></td>
<td><p>Two DWORD-sized values representing a pen plotter's <em>x</em> and <em>y</em> resolution, in dots per inch.</p></td>
<td><p></p>
{1016,
1016}</td>
</tr>
<tr class="even">
<td><p><strong>PlotPenData</strong></p></td>
<td><p>A pen description for each pen. For more information, see the <strong>Pen Descriptions</strong> section that follows this Table.</p></td>
<td><p>None.</p></td>
</tr>
<tr class="odd">
<td><p><strong>PushPopPal</strong></p></td>
<td><p>1=Driver must push/pop palette when switching between RTL and HPGL2.</p>
<p>0=Push/pop is not required.</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>RasterByteAlign</strong></p></td>
<td><p>1=Device must receive all raster data on byte-aligned x coordinates.</p>
<p>0=Byte alignment is not required.</p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>RasterCap</strong></p></td>
<td><p>1=Raster device</p>
<p>0=Pen device</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>RasterDPI</strong></p></td>
<td><p>Two DWORD-sized values representing <em>x</em> and <em>y</em> resolution, in dots per inch.</p>
<p>For raster plotters, this is the raster resolution.</p>
<p>For pen plotters, this is the ideal resolution the GDI supplies to an application.</p></td>
<td><p></p>
{300,
300}</td>
</tr>
<tr class="odd">
<td><p><strong>RollFeedCap</strong></p></td>
<td><p>1=Device has roll paper source.</p>
<p>0=No support.</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>ROPLevel</strong></p></td>
<td><p>ROP_LEVEL_0 = No RasterOp support.</p>
<p>ROP_LEVEL_1 = Rop1 support.</p>
<p>ROP_LEVEL_2 = Rop2 support.</p>
<p>ROP_LEVEL_3 = Rop3 support.</p></td>
<td><p>ROP_LEVEL_0</p></td>
</tr>
<tr class="odd">
<td><p><strong>RTLMonoEncode5</strong></p></td>
<td><p>1=HP Raster Transfer Language (RTL) Monochrome Compression Mode 5 is supported.</p>
<p>0=No support.</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>RTLMonoFixPal</strong></p></td>
<td><p>RTL Monochrome palette only.</p>
<p>0=White, 1=Black</p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>RTLMonoNoCID</strong></p></td>
<td><p>1=In RTL Mono mode, CID commands are not required.</p>
<p>0=In RTL Mono mode, CID commands are required.</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>RTLNoDPIxy</strong></p></td>
<td><p>1=RTL DPI X,Y move commands are not supported.</p>
<p>0=These commands are supported.</p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>TransparentCap</strong></p></td>
<td><p>1=Device supports transparent mode.</p>
<p>0=No support.</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>WindingFillCap</strong></p></td>
<td><p>1=Device supports winding fills.</p>
<p>0=No support.</p></td>
<td><p>0</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-pen-descriptions-gg"></a>Pen Descriptions

Each pen description must have the following format:

**PlotPenData {***Pen Number***,** *Color***}**

where *Pen Number* identifies the pen's slot number and *Color* is a PC\_IDX\_-prefixed color identifier. Following are example pen descriptions:

```
PlotPenData {1, PC_IDX_WHITE}
PlotPenData {2, PC_IDX_BLACK}
PlotPenData {3, PC_IDX_RED}
```

### <a href="" id="ddk-form-descriptions-gg"></a>Form Descriptions

Each form description must have the following format:

**FormInfo {"***Form Description***",** *Width***,** *Length***,** *Left Margin***,** *Top Margin***,** *Right Margin***,** *Bottom Margin***}**

where *Form Description* is a string describing the form, *Width* and *Length* specify the form size in 1/1000 mm units, and the margins are also specified in 1/1000 mm units. Following are three examples:

```
FormInfo {"Roll Paper 24 in",    609600,      0, 0, 0, 0, 0}
FormInfo {"ANSI A 8.5 x 11 in",  215900, 279400, 0, 0, 0, 0}
FormInfo {"ISO A4 210 x 297 mm", 210000, 297000, 0, 0, 0, 0}
```

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bprint\print%5D:%20PCD%20Source%20File%20Format%20%20RELEASE:%20%289/1/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")

