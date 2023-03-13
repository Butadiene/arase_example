#
tutorial url
https://github.com/ergsc-devel/arase_example

# install?

for VSCode
First, 

```
!pip install pyspedas
```

changes here.

```
%pip install pyspedas
%matplotlib widget
```

and run Arase_data_examples in order, we can get plots


# Memo

Arase_data_examples.ipynbをいじる。

## pytplot
tplot(IDL)のpython版らしい。
https://pytplot.readthedocs.io/en/latest/introduction.html
だれかが作ってる。名大ではなさそう。

## mgf 
mgf 観測機器の名前。
```
from pyspedas.erg import mgf
```
で、この観測機器(今回はergのmgf)のデータを落とすことができる。
具体的に：
mgfメソッド（関数？）は落ちてきたデータをcdfファイル形式で保存する。返り値は多分使うことはなさげ？

tplot変数：時刻変数、メタデータなどを全部含んだデータ構造体。

## timespan
バグ発生中


```
pytplot.timespan( '2017-03-27 09:00:00', 6, keyword='hours' )
tplot( [ 'erg_mgf_l2_mag_8sec_sm', 'erg_mgf_l2_mag_8sec_gsm' ] )
```
では動かない。

```
pytplot.timespan( '2017-03-27 09:00:00', 6, keyword='hours' )
pytplot.xlim('2017-03-27 09:00:00', '2017-03-27 15:00:00')
tplot( [ 'erg_mgf_l2_mag_8sec_sm', 'erg_mgf_l2_mag_8sec_gsm' ] )
```

に変更する。(xlimがある場合、tplotがなくても大丈夫)


## ylim
動かない。

```
pytplot.ylim( 'erg_mgf_l2_mag_8sec_sm', -300., 300. )
tplot( [ 'erg_mgf_l2_mag_8sec_sm' ] )
```

はダメ。

```
pytplot.options( 'erg_mgf_l2_mag_8sec_sm', 'yrange', [-100, 100])
tplot( [ 'erg_mgf_l2_mag_8sec_sm' ] )
```
にする。

## tplot
オブジェクト。pytplot.tplot

こいつが観測機器の関数で実行されたtplot関係のデータを「全て」持ってる。

機器の関数を実行すると、tplotの中に格納される。
```
pytplot.tplot_names()
```
を実行すると、これが出てくる
```
0 : erg_mgf_l2_epoch_8sec
1 : erg_mgf_l2_mag_8sec_dsi
2 : erg_mgf_l2_mag_8sec_gse
3 : erg_mgf_l2_mag_8sec_gsm
4 : erg_mgf_l2_mag_8sec_sm
5 : erg_mgf_l2_magt_8sec
6 : erg_mgf_l2_rmsd_8sec_dsi
7 : erg_mgf_l2_rmsd_8sec_gse
8 : erg_mgf_l2_rmsd_8sec_gsm
9 : erg_mgf_l2_rmsd_8sec_sm
10 : erg_mgf_l2_rmsd_8sec
11 : erg_mgf_l2_n_rmsd_8sec
12 : erg_mgf_l2_dyn_rng_8sec
13 : erg_mgf_l2_quality_8sec
14 : erg_mgf_l2_quality_8sec_gc
15 : erg_mgf_l2_igrf_8sec_dsi
16 : erg_mgf_l2_igrf_8sec_gse
17 : erg_mgf_l2_igrf_8sec_gsm
18 : erg_mgf_l2_igrf_8sec_sm
19 : erg_pwe_ofa_l2_spec_epoch_e132
20 : erg_pwe_ofa_l2_spec_E_spectra_132
21 : erg_pwe_ofa_l2_spec_quality_flag_e132
22 : erg_pwe_ofa_l2_spec_epoch_b132
23 : erg_pwe_ofa_l2_spec_B_spectra_132
24 : erg_pwe_ofa_l2_spec_quality_flag_b132
```

というのがそういう意味

# Question 
