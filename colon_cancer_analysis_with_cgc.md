```python
#import the packages
import pandas as pd
import numpy as np
```


```python
#Read the combined file of colon_cancer_mutation
colon_mutation_data=pd.read_table('colon_mutation_poly_sift_score.txt', sep='\t')
colon_mutation_data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>seqnames</th>
      <th>start</th>
      <th>end</th>
      <th>width</th>
      <th>strand</th>
      <th>AD</th>
      <th>AD.1</th>
      <th>AF</th>
      <th>Consequence</th>
      <th>IMPACT</th>
      <th>...</th>
      <th>HGVSc</th>
      <th>HGVSp</th>
      <th>CLIN_SIG</th>
      <th>PolyPhen</th>
      <th>SIFT</th>
      <th>SampleID</th>
      <th>POLYPHEN</th>
      <th>POLYSCORE</th>
      <th>SIFTS</th>
      <th>SIFTSCORE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>16736303</td>
      <td>16736303</td>
      <td>1</td>
      <td>*</td>
      <td>20</td>
      <td>3</td>
      <td>0.130</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENST00000335496.1:c.380T&gt;C</td>
      <td>ENSP00000335612.1:p.Leu127Pro</td>
      <td>NaN</td>
      <td>possibly_damaging(0.894)</td>
      <td>deleterious(0)</td>
      <td>eAPD114</td>
      <td>possibly_damaging</td>
      <td>0.894</td>
      <td>deleterious</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>23836607</td>
      <td>23836607</td>
      <td>1</td>
      <td>*</td>
      <td>15</td>
      <td>3</td>
      <td>0.167</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENST00000361729.2:c.1079C&gt;T</td>
      <td>ENSP00000355249.2:p.Pro360Leu</td>
      <td>NaN</td>
      <td>benign(0)</td>
      <td>tolerated(0.48)</td>
      <td>eAPD114</td>
      <td>benign</td>
      <td>0.000</td>
      <td>tolerated</td>
      <td>0.48</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>27701288</td>
      <td>27701288</td>
      <td>1</td>
      <td>*</td>
      <td>12</td>
      <td>6</td>
      <td>0.333</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENST00000270879.4:c.22C&gt;T</td>
      <td>ENSP00000270879.4:p.Pro8Ser</td>
      <td>NaN</td>
      <td>benign(0)</td>
      <td>tolerated(0.2)</td>
      <td>eAPD114</td>
      <td>benign</td>
      <td>0.000</td>
      <td>tolerated</td>
      <td>0.20</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>32800671</td>
      <td>32800671</td>
      <td>1</td>
      <td>*</td>
      <td>12</td>
      <td>3</td>
      <td>0.200</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENST00000329421.7:c.115G&gt;A</td>
      <td>ENSP00000362638.4:p.Asp39Asn</td>
      <td>NaN</td>
      <td>probably_damaging(1)</td>
      <td>deleterious(0.04)</td>
      <td>eAPD114</td>
      <td>probably_damaging</td>
      <td>1.000</td>
      <td>deleterious</td>
      <td>0.04</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>70644607</td>
      <td>70644607</td>
      <td>1</td>
      <td>*</td>
      <td>14</td>
      <td>4</td>
      <td>0.222</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENST00000370952.3:c.731C&gt;T</td>
      <td>ENSP00000359990.3:p.Ser244Leu</td>
      <td>NaN</td>
      <td>possibly_damaging(0.831)</td>
      <td>deleterious(0.01)</td>
      <td>eAPD114</td>
      <td>possibly_damaging</td>
      <td>0.831</td>
      <td>deleterious</td>
      <td>0.01</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>73389</th>
      <td>22</td>
      <td>29536275</td>
      <td>29536275</td>
      <td>1</td>
      <td>*</td>
      <td>58</td>
      <td>4</td>
      <td>0.065</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENST00000327813.5:c.1180A&gt;G</td>
      <td>ENSP00000331242.5:p.Thr394Ala</td>
      <td>NaN</td>
      <td>probably_damaging(0.994)</td>
      <td>deleterious_low_confidence(0.01)</td>
      <td>eAPD081</td>
      <td>probably_damaging</td>
      <td>0.994</td>
      <td>deleterious_low_confidence</td>
      <td>0.01</td>
    </tr>
    <tr>
      <th>73390</th>
      <td>1</td>
      <td>200569584</td>
      <td>200569584</td>
      <td>1</td>
      <td>*</td>
      <td>24</td>
      <td>11</td>
      <td>0.324</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENST00000367350.4:c.2200C&gt;T</td>
      <td>ENSP00000356319.4:p.Arg734Trp</td>
      <td>NaN</td>
      <td>possibly_damaging(0.517)</td>
      <td>tolerated(0.12)</td>
      <td>eAPD081</td>
      <td>possibly_damaging</td>
      <td>0.517</td>
      <td>tolerated</td>
      <td>0.12</td>
    </tr>
    <tr>
      <th>73391</th>
      <td>5</td>
      <td>63802465</td>
      <td>63802465</td>
      <td>1</td>
      <td>*</td>
      <td>29</td>
      <td>10</td>
      <td>0.262</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENST00000334025.2:c.14C&gt;T</td>
      <td>ENSP00000334851.2:p.Pro5Leu</td>
      <td>NaN</td>
      <td>benign(0.039)</td>
      <td>tolerated_low_confidence(0.07)</td>
      <td>eAPD081</td>
      <td>benign</td>
      <td>0.039</td>
      <td>tolerated_low_confidence</td>
      <td>0.07</td>
    </tr>
    <tr>
      <th>73392</th>
      <td>5</td>
      <td>140531231</td>
      <td>140531231</td>
      <td>1</td>
      <td>*</td>
      <td>86</td>
      <td>24</td>
      <td>0.223</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENST00000231136.1:c.1393G&gt;A</td>
      <td>ENSP00000231136.1:p.Ala465Thr</td>
      <td>NaN</td>
      <td>probably_damaging(0.996)</td>
      <td>deleterious_low_confidence(0)</td>
      <td>eAPD081</td>
      <td>probably_damaging</td>
      <td>0.996</td>
      <td>deleterious_low_confidence</td>
      <td>0.00</td>
    </tr>
    <tr>
      <th>73393</th>
      <td>18</td>
      <td>61305310</td>
      <td>61305310</td>
      <td>1</td>
      <td>*</td>
      <td>70</td>
      <td>18</td>
      <td>0.211</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENST00000341074.5:c.816G&gt;T</td>
      <td>ENSP00000343445.5:p.Leu272Phe</td>
      <td>NaN</td>
      <td>benign(0.411)</td>
      <td>deleterious(0.02)</td>
      <td>eAPD081</td>
      <td>benign</td>
      <td>0.411</td>
      <td>deleterious</td>
      <td>0.02</td>
    </tr>
  </tbody>
</table>
<p>73394 rows × 21 columns</p>
</div>




```python
#Read Cancer Gene Census Symbols
CGC = pd.read_table('cgc_gene_symbol.txt', sep='\t')
CGC
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SYMBOL</th>
      <th>CancerGeneCensus</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A1CF</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ABI1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ABL1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ABL2</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ACKR3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>718</th>
      <td>ZNF429</td>
      <td>1</td>
    </tr>
    <tr>
      <th>719</th>
      <td>ZNF479</td>
      <td>1</td>
    </tr>
    <tr>
      <th>720</th>
      <td>ZNF521</td>
      <td>1</td>
    </tr>
    <tr>
      <th>721</th>
      <td>ZNRF3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>722</th>
      <td>ZRSR2</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>723 rows × 2 columns</p>
</div>




```python
#Append the CGC genes to the colon mutation table
cgc_mapped = pd.merge(colon_mutation_data,CGC, on='SYMBOL', how ='left')
cgc_mapped
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>seqnames</th>
      <th>start</th>
      <th>end</th>
      <th>width</th>
      <th>strand</th>
      <th>AD</th>
      <th>AD.1</th>
      <th>AF</th>
      <th>Consequence</th>
      <th>IMPACT</th>
      <th>...</th>
      <th>HGVSp</th>
      <th>CLIN_SIG</th>
      <th>PolyPhen</th>
      <th>SIFT</th>
      <th>SampleID</th>
      <th>POLYPHEN</th>
      <th>POLYSCORE</th>
      <th>SIFTS</th>
      <th>SIFTSCORE</th>
      <th>CancerGeneCensus</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>16736303</td>
      <td>16736303</td>
      <td>1</td>
      <td>*</td>
      <td>20</td>
      <td>3</td>
      <td>0.130</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENSP00000335612.1:p.Leu127Pro</td>
      <td>NaN</td>
      <td>possibly_damaging(0.894)</td>
      <td>deleterious(0)</td>
      <td>eAPD114</td>
      <td>possibly_damaging</td>
      <td>0.894</td>
      <td>deleterious</td>
      <td>0.00</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>23836607</td>
      <td>23836607</td>
      <td>1</td>
      <td>*</td>
      <td>15</td>
      <td>3</td>
      <td>0.167</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENSP00000355249.2:p.Pro360Leu</td>
      <td>NaN</td>
      <td>benign(0)</td>
      <td>tolerated(0.48)</td>
      <td>eAPD114</td>
      <td>benign</td>
      <td>0.000</td>
      <td>tolerated</td>
      <td>0.48</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>27701288</td>
      <td>27701288</td>
      <td>1</td>
      <td>*</td>
      <td>12</td>
      <td>6</td>
      <td>0.333</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENSP00000270879.4:p.Pro8Ser</td>
      <td>NaN</td>
      <td>benign(0)</td>
      <td>tolerated(0.2)</td>
      <td>eAPD114</td>
      <td>benign</td>
      <td>0.000</td>
      <td>tolerated</td>
      <td>0.20</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>32800671</td>
      <td>32800671</td>
      <td>1</td>
      <td>*</td>
      <td>12</td>
      <td>3</td>
      <td>0.200</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENSP00000362638.4:p.Asp39Asn</td>
      <td>NaN</td>
      <td>probably_damaging(1)</td>
      <td>deleterious(0.04)</td>
      <td>eAPD114</td>
      <td>probably_damaging</td>
      <td>1.000</td>
      <td>deleterious</td>
      <td>0.04</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>70644607</td>
      <td>70644607</td>
      <td>1</td>
      <td>*</td>
      <td>14</td>
      <td>4</td>
      <td>0.222</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENSP00000359990.3:p.Ser244Leu</td>
      <td>NaN</td>
      <td>possibly_damaging(0.831)</td>
      <td>deleterious(0.01)</td>
      <td>eAPD114</td>
      <td>possibly_damaging</td>
      <td>0.831</td>
      <td>deleterious</td>
      <td>0.01</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>73389</th>
      <td>22</td>
      <td>29536275</td>
      <td>29536275</td>
      <td>1</td>
      <td>*</td>
      <td>58</td>
      <td>4</td>
      <td>0.065</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENSP00000331242.5:p.Thr394Ala</td>
      <td>NaN</td>
      <td>probably_damaging(0.994)</td>
      <td>deleterious_low_confidence(0.01)</td>
      <td>eAPD081</td>
      <td>probably_damaging</td>
      <td>0.994</td>
      <td>deleterious_low_confidence</td>
      <td>0.01</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>73390</th>
      <td>1</td>
      <td>200569584</td>
      <td>200569584</td>
      <td>1</td>
      <td>*</td>
      <td>24</td>
      <td>11</td>
      <td>0.324</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENSP00000356319.4:p.Arg734Trp</td>
      <td>NaN</td>
      <td>possibly_damaging(0.517)</td>
      <td>tolerated(0.12)</td>
      <td>eAPD081</td>
      <td>possibly_damaging</td>
      <td>0.517</td>
      <td>tolerated</td>
      <td>0.12</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>73391</th>
      <td>5</td>
      <td>63802465</td>
      <td>63802465</td>
      <td>1</td>
      <td>*</td>
      <td>29</td>
      <td>10</td>
      <td>0.262</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENSP00000334851.2:p.Pro5Leu</td>
      <td>NaN</td>
      <td>benign(0.039)</td>
      <td>tolerated_low_confidence(0.07)</td>
      <td>eAPD081</td>
      <td>benign</td>
      <td>0.039</td>
      <td>tolerated_low_confidence</td>
      <td>0.07</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>73392</th>
      <td>5</td>
      <td>140531231</td>
      <td>140531231</td>
      <td>1</td>
      <td>*</td>
      <td>86</td>
      <td>24</td>
      <td>0.223</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENSP00000231136.1:p.Ala465Thr</td>
      <td>NaN</td>
      <td>probably_damaging(0.996)</td>
      <td>deleterious_low_confidence(0)</td>
      <td>eAPD081</td>
      <td>probably_damaging</td>
      <td>0.996</td>
      <td>deleterious_low_confidence</td>
      <td>0.00</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>73393</th>
      <td>18</td>
      <td>61305310</td>
      <td>61305310</td>
      <td>1</td>
      <td>*</td>
      <td>70</td>
      <td>18</td>
      <td>0.211</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENSP00000343445.5:p.Leu272Phe</td>
      <td>NaN</td>
      <td>benign(0.411)</td>
      <td>deleterious(0.02)</td>
      <td>eAPD081</td>
      <td>benign</td>
      <td>0.411</td>
      <td>deleterious</td>
      <td>0.02</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>73394 rows × 22 columns</p>
</div>




```python
#Check how many are mapped to CGC
cgi_pass_variants = cgc_mapped[cgc_mapped['CancerGeneCensus']==1]
cgi_pass_variants

#There were 4601 positions mapped with duplicates
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>seqnames</th>
      <th>start</th>
      <th>end</th>
      <th>width</th>
      <th>strand</th>
      <th>AD</th>
      <th>AD.1</th>
      <th>AF</th>
      <th>Consequence</th>
      <th>IMPACT</th>
      <th>...</th>
      <th>HGVSp</th>
      <th>CLIN_SIG</th>
      <th>PolyPhen</th>
      <th>SIFT</th>
      <th>SampleID</th>
      <th>POLYPHEN</th>
      <th>POLYSCORE</th>
      <th>SIFTS</th>
      <th>SIFTSCORE</th>
      <th>CancerGeneCensus</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>32</th>
      <td>7</td>
      <td>151896387</td>
      <td>151896387</td>
      <td>1</td>
      <td>*</td>
      <td>14</td>
      <td>3</td>
      <td>0.176</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENSP00000262189.6:p.Ala1417Val</td>
      <td>NaN</td>
      <td>benign(0.039)</td>
      <td>tolerated(0.12)</td>
      <td>eAPD114</td>
      <td>benign</td>
      <td>0.039</td>
      <td>tolerated</td>
      <td>0.12</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>35</th>
      <td>10</td>
      <td>61574409</td>
      <td>61574409</td>
      <td>1</td>
      <td>*</td>
      <td>19</td>
      <td>4</td>
      <td>0.174</td>
      <td>splice_donor_variant</td>
      <td>HIGH</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>eAPD114</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>68</th>
      <td>19</td>
      <td>10597428</td>
      <td>10597428</td>
      <td>1</td>
      <td>*</td>
      <td>17</td>
      <td>3</td>
      <td>0.150</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENSP00000171111.4:p.Ser592Asn</td>
      <td>NaN</td>
      <td>benign(0.001)</td>
      <td>tolerated(0.43)</td>
      <td>eAPD114</td>
      <td>benign</td>
      <td>0.001</td>
      <td>tolerated</td>
      <td>0.43</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>79</th>
      <td>22</td>
      <td>22160176</td>
      <td>22160176</td>
      <td>1</td>
      <td>*</td>
      <td>12</td>
      <td>3</td>
      <td>0.200</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENSP00000215832.6:p.Pro152Leu</td>
      <td>NaN</td>
      <td>probably_damaging(0.926)</td>
      <td>deleterious(0.03)</td>
      <td>eAPD114</td>
      <td>probably_damaging</td>
      <td>0.926</td>
      <td>deleterious</td>
      <td>0.03</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>88</th>
      <td>1</td>
      <td>120457988</td>
      <td>120457988</td>
      <td>1</td>
      <td>*</td>
      <td>15</td>
      <td>4</td>
      <td>0.236</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENSP00000256646.2:p.Arg2453Trp</td>
      <td>NaN</td>
      <td>probably_damaging(0.948)</td>
      <td>deleterious(0.04)</td>
      <td>eAPD114</td>
      <td>probably_damaging</td>
      <td>0.948</td>
      <td>deleterious</td>
      <td>0.04</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>73322</th>
      <td>12</td>
      <td>25398284</td>
      <td>25398284</td>
      <td>1</td>
      <td>*</td>
      <td>28</td>
      <td>5</td>
      <td>0.152</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENSP00000256078.4:p.Gly12Val</td>
      <td>pathogenic&amp;pathogenic/likely_pathogenic&amp;likely...</td>
      <td>probably_damaging(0.972)</td>
      <td>deleterious(0)</td>
      <td>eAPD079</td>
      <td>probably_damaging</td>
      <td>0.972</td>
      <td>deleterious</td>
      <td>0.00</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73339</th>
      <td>17</td>
      <td>7578263</td>
      <td>7578263</td>
      <td>1</td>
      <td>*</td>
      <td>15</td>
      <td>8</td>
      <td>0.348</td>
      <td>stop_gained</td>
      <td>HIGH</td>
      <td>...</td>
      <td>ENSP00000269305.4:p.Arg196Ter</td>
      <td>pathogenic</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>eAPD079</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73340</th>
      <td>17</td>
      <td>58740668</td>
      <td>58740668</td>
      <td>1</td>
      <td>*</td>
      <td>19</td>
      <td>6</td>
      <td>0.240</td>
      <td>stop_gained</td>
      <td>HIGH</td>
      <td>...</td>
      <td>ENSP00000306682.2:p.Glu525Ter</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>eAPD079</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73358</th>
      <td>X</td>
      <td>152845446</td>
      <td>152845446</td>
      <td>1</td>
      <td>*</td>
      <td>20</td>
      <td>8</td>
      <td>0.286</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENSP00000263519.4:p.Val1118Ala</td>
      <td>NaN</td>
      <td>possibly_damaging(0.889)</td>
      <td>deleterious(0.03)</td>
      <td>eAPD079</td>
      <td>possibly_damaging</td>
      <td>0.889</td>
      <td>deleterious</td>
      <td>0.03</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73387</th>
      <td>17</td>
      <td>7578524</td>
      <td>7578524</td>
      <td>1</td>
      <td>*</td>
      <td>41</td>
      <td>11</td>
      <td>0.212</td>
      <td>stop_gained</td>
      <td>HIGH</td>
      <td>...</td>
      <td>ENSP00000269305.4:p.Gln136Ter</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>eAPD081</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
<p>4601 rows × 22 columns</p>
</div>




```python
#Select required columns from the dataframe
cgi_selected = cgi_pass_variants[['SYMBOL', 'seqnames', 'start', 'end','CLIN_SIG',
                                                    'Consequence', 'IMPACT', 'SIFTS', 'POLYPHEN', 'CancerGeneCensus']]

cgi_selected
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SYMBOL</th>
      <th>seqnames</th>
      <th>start</th>
      <th>end</th>
      <th>CLIN_SIG</th>
      <th>Consequence</th>
      <th>IMPACT</th>
      <th>SIFTS</th>
      <th>POLYPHEN</th>
      <th>CancerGeneCensus</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>32</th>
      <td>KMT2C</td>
      <td>7</td>
      <td>151896387</td>
      <td>151896387</td>
      <td>NaN</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>tolerated</td>
      <td>benign</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>35</th>
      <td>CCDC6</td>
      <td>10</td>
      <td>61574409</td>
      <td>61574409</td>
      <td>NaN</td>
      <td>splice_donor_variant</td>
      <td>HIGH</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>68</th>
      <td>KEAP1</td>
      <td>19</td>
      <td>10597428</td>
      <td>10597428</td>
      <td>NaN</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>tolerated</td>
      <td>benign</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>79</th>
      <td>MAPK1</td>
      <td>22</td>
      <td>22160176</td>
      <td>22160176</td>
      <td>NaN</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>deleterious</td>
      <td>probably_damaging</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>88</th>
      <td>NOTCH2</td>
      <td>1</td>
      <td>120457988</td>
      <td>120457988</td>
      <td>NaN</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>deleterious</td>
      <td>probably_damaging</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>73322</th>
      <td>KRAS</td>
      <td>12</td>
      <td>25398284</td>
      <td>25398284</td>
      <td>pathogenic&amp;pathogenic/likely_pathogenic&amp;likely...</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>deleterious</td>
      <td>probably_damaging</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73339</th>
      <td>TP53</td>
      <td>17</td>
      <td>7578263</td>
      <td>7578263</td>
      <td>pathogenic</td>
      <td>stop_gained</td>
      <td>HIGH</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73340</th>
      <td>PPM1D</td>
      <td>17</td>
      <td>58740668</td>
      <td>58740668</td>
      <td>NaN</td>
      <td>stop_gained</td>
      <td>HIGH</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73358</th>
      <td>ATP2B3</td>
      <td>X</td>
      <td>152845446</td>
      <td>152845446</td>
      <td>NaN</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>deleterious</td>
      <td>possibly_damaging</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73387</th>
      <td>TP53</td>
      <td>17</td>
      <td>7578524</td>
      <td>7578524</td>
      <td>NaN</td>
      <td>stop_gained</td>
      <td>HIGH</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
<p>4601 rows × 10 columns</p>
</div>




```python
#Fill empty columns of polyphen , sift and clinvar with 0
cgi_selected['CLIN_SIG'].fillna(0, inplace=True)
cgi_selected['POLYPHEN'].fillna(0, inplace=True)
cgi_selected['SIFTS'].fillna(0, inplace=True)
```

    /home/molmed/anaconda3/lib/python3.7/site-packages/pandas/core/generic.py:6287: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      self._update_inplace(new_data)



```python
#replace non-pathogenic values of polyphen with 0
cgi_poly=cgi_selected.replace(to_replace =["benign", "possibly_damaging","unknown"], 
                            value =0)

##replace pathogenic values of polyphen with 1
cgi_poly=cgi_poly.replace(to_replace =["probably_damaging"], 
                            value =1)
#view the update
cgi_poly
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SYMBOL</th>
      <th>seqnames</th>
      <th>start</th>
      <th>end</th>
      <th>CLIN_SIG</th>
      <th>Consequence</th>
      <th>IMPACT</th>
      <th>SIFTS</th>
      <th>POLYPHEN</th>
      <th>CancerGeneCensus</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>32</th>
      <td>KMT2C</td>
      <td>7</td>
      <td>151896387</td>
      <td>151896387</td>
      <td>0</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>tolerated</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>35</th>
      <td>CCDC6</td>
      <td>10</td>
      <td>61574409</td>
      <td>61574409</td>
      <td>0</td>
      <td>splice_donor_variant</td>
      <td>HIGH</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>68</th>
      <td>KEAP1</td>
      <td>19</td>
      <td>10597428</td>
      <td>10597428</td>
      <td>0</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>tolerated</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>79</th>
      <td>MAPK1</td>
      <td>22</td>
      <td>22160176</td>
      <td>22160176</td>
      <td>0</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>deleterious</td>
      <td>1</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>88</th>
      <td>NOTCH2</td>
      <td>1</td>
      <td>120457988</td>
      <td>120457988</td>
      <td>0</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>deleterious</td>
      <td>1</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>73322</th>
      <td>KRAS</td>
      <td>12</td>
      <td>25398284</td>
      <td>25398284</td>
      <td>pathogenic&amp;pathogenic/likely_pathogenic&amp;likely...</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>deleterious</td>
      <td>1</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73339</th>
      <td>TP53</td>
      <td>17</td>
      <td>7578263</td>
      <td>7578263</td>
      <td>pathogenic</td>
      <td>stop_gained</td>
      <td>HIGH</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73340</th>
      <td>PPM1D</td>
      <td>17</td>
      <td>58740668</td>
      <td>58740668</td>
      <td>0</td>
      <td>stop_gained</td>
      <td>HIGH</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73358</th>
      <td>ATP2B3</td>
      <td>X</td>
      <td>152845446</td>
      <td>152845446</td>
      <td>0</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>deleterious</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73387</th>
      <td>TP53</td>
      <td>17</td>
      <td>7578524</td>
      <td>7578524</td>
      <td>0</td>
      <td>stop_gained</td>
      <td>HIGH</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
<p>4601 rows × 10 columns</p>
</div>




```python
#replace non-pathogenic values of SIFT with 0
cgi_poly_sift=cgi_poly.replace(to_replace =["tolerated", "deleterious_low_confidence","tolerated_low_confidence"], 
                            value =0)

##replace pathogenic values of SIFT with 1
cgi_poly_sift=cgi_poly_sift.replace(to_replace =["deleterious"], 
                            value =1)
#View the updates
cgi_poly_sift
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SYMBOL</th>
      <th>seqnames</th>
      <th>start</th>
      <th>end</th>
      <th>CLIN_SIG</th>
      <th>Consequence</th>
      <th>IMPACT</th>
      <th>SIFTS</th>
      <th>POLYPHEN</th>
      <th>CancerGeneCensus</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>32</th>
      <td>KMT2C</td>
      <td>7</td>
      <td>151896387</td>
      <td>151896387</td>
      <td>0</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>35</th>
      <td>CCDC6</td>
      <td>10</td>
      <td>61574409</td>
      <td>61574409</td>
      <td>0</td>
      <td>splice_donor_variant</td>
      <td>HIGH</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>68</th>
      <td>KEAP1</td>
      <td>19</td>
      <td>10597428</td>
      <td>10597428</td>
      <td>0</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>79</th>
      <td>MAPK1</td>
      <td>22</td>
      <td>22160176</td>
      <td>22160176</td>
      <td>0</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1</td>
      <td>1</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>88</th>
      <td>NOTCH2</td>
      <td>1</td>
      <td>120457988</td>
      <td>120457988</td>
      <td>0</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1</td>
      <td>1</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>73322</th>
      <td>KRAS</td>
      <td>12</td>
      <td>25398284</td>
      <td>25398284</td>
      <td>pathogenic&amp;pathogenic/likely_pathogenic&amp;likely...</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1</td>
      <td>1</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73339</th>
      <td>TP53</td>
      <td>17</td>
      <td>7578263</td>
      <td>7578263</td>
      <td>pathogenic</td>
      <td>stop_gained</td>
      <td>HIGH</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73340</th>
      <td>PPM1D</td>
      <td>17</td>
      <td>58740668</td>
      <td>58740668</td>
      <td>0</td>
      <td>stop_gained</td>
      <td>HIGH</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73358</th>
      <td>ATP2B3</td>
      <td>X</td>
      <td>152845446</td>
      <td>152845446</td>
      <td>0</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73387</th>
      <td>TP53</td>
      <td>17</td>
      <td>7578524</td>
      <td>7578524</td>
      <td>0</td>
      <td>stop_gained</td>
      <td>HIGH</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
<p>4601 rows × 10 columns</p>
</div>




```python
#Assign clinvar as 1 when it reports pathogenic
cgi_poly_sift.loc[cgi_poly_sift['CLIN_SIG'].str.contains('pathogenic', na=False), 'CLIN_SIG'] = 1
cgi_poly_sift
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SYMBOL</th>
      <th>seqnames</th>
      <th>start</th>
      <th>end</th>
      <th>CLIN_SIG</th>
      <th>Consequence</th>
      <th>IMPACT</th>
      <th>SIFTS</th>
      <th>POLYPHEN</th>
      <th>CancerGeneCensus</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>32</th>
      <td>KMT2C</td>
      <td>7</td>
      <td>151896387</td>
      <td>151896387</td>
      <td>0</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>35</th>
      <td>CCDC6</td>
      <td>10</td>
      <td>61574409</td>
      <td>61574409</td>
      <td>0</td>
      <td>splice_donor_variant</td>
      <td>HIGH</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>68</th>
      <td>KEAP1</td>
      <td>19</td>
      <td>10597428</td>
      <td>10597428</td>
      <td>0</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>79</th>
      <td>MAPK1</td>
      <td>22</td>
      <td>22160176</td>
      <td>22160176</td>
      <td>0</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1</td>
      <td>1</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>88</th>
      <td>NOTCH2</td>
      <td>1</td>
      <td>120457988</td>
      <td>120457988</td>
      <td>0</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1</td>
      <td>1</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>73322</th>
      <td>KRAS</td>
      <td>12</td>
      <td>25398284</td>
      <td>25398284</td>
      <td>1</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1</td>
      <td>1</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73339</th>
      <td>TP53</td>
      <td>17</td>
      <td>7578263</td>
      <td>7578263</td>
      <td>1</td>
      <td>stop_gained</td>
      <td>HIGH</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73340</th>
      <td>PPM1D</td>
      <td>17</td>
      <td>58740668</td>
      <td>58740668</td>
      <td>0</td>
      <td>stop_gained</td>
      <td>HIGH</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73358</th>
      <td>ATP2B3</td>
      <td>X</td>
      <td>152845446</td>
      <td>152845446</td>
      <td>0</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73387</th>
      <td>TP53</td>
      <td>17</td>
      <td>7578524</td>
      <td>7578524</td>
      <td>0</td>
      <td>stop_gained</td>
      <td>HIGH</td>
      <td>0</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
<p>4601 rows × 10 columns</p>
</div>




```python
#Filter CGC by support of any two SIFT, clinvar or Polyphen

#Select the data by polyphen and sift
poly_sift = cgi_poly_sift[(cgi_poly_sift.POLYPHEN == 1) & (cgi_poly_sift.SIFTS == 1)]

#Select the data by polyphen and CLIN_SIG
poly_clin = cgi_poly_sift[(cgi_poly_sift.POLYPHEN == 1) & (cgi_poly_sift.CLIN_SIG == 1)]

#Select the data by CLIN_SIG and sift
clin_sift = cgi_poly_sift[(cgi_poly_sift.CLIN_SIG == 1) & (cgi_poly_sift.SIFTS == 1)]

```


```python
#Concatenate the master deleterious position
frames = [poly_sift, poly_clin, clin_sift]
master_pos = pd.concat(frames)
master_pos
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SYMBOL</th>
      <th>seqnames</th>
      <th>start</th>
      <th>end</th>
      <th>CLIN_SIG</th>
      <th>Consequence</th>
      <th>IMPACT</th>
      <th>SIFTS</th>
      <th>POLYPHEN</th>
      <th>CancerGeneCensus</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>79</th>
      <td>MAPK1</td>
      <td>22</td>
      <td>22160176</td>
      <td>22160176</td>
      <td>0</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1</td>
      <td>1</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>88</th>
      <td>NOTCH2</td>
      <td>1</td>
      <td>120457988</td>
      <td>120457988</td>
      <td>0</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1</td>
      <td>1</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>257</th>
      <td>LRP1B</td>
      <td>2</td>
      <td>141526827</td>
      <td>141526827</td>
      <td>0</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1</td>
      <td>1</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>328</th>
      <td>KIT</td>
      <td>4</td>
      <td>55602705</td>
      <td>55602705</td>
      <td>0</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1</td>
      <td>1</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>344</th>
      <td>MAP3K1</td>
      <td>5</td>
      <td>56180572</td>
      <td>56180572</td>
      <td>0</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1</td>
      <td>1</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>71897</th>
      <td>SMAD4</td>
      <td>18</td>
      <td>48604787</td>
      <td>48604787</td>
      <td>1</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1</td>
      <td>1</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>71920</th>
      <td>PIK3CA</td>
      <td>3</td>
      <td>178936094</td>
      <td>178936094</td>
      <td>1</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73223</th>
      <td>PIK3CA</td>
      <td>3</td>
      <td>178916930</td>
      <td>178916930</td>
      <td>1</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1</td>
      <td>1</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73244</th>
      <td>KRAS</td>
      <td>12</td>
      <td>25398284</td>
      <td>25398284</td>
      <td>1</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1</td>
      <td>0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73322</th>
      <td>KRAS</td>
      <td>12</td>
      <td>25398284</td>
      <td>25398284</td>
      <td>1</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1</td>
      <td>1</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
<p>1340 rows × 10 columns</p>
</div>




```python
#select required columns in the master positions
master_pos_sel = master_pos[["SYMBOL","seqnames","start","end"]]
master_pos_sel = master_pos_sel.drop_duplicates()
master_pos_sel

#There are 1068 unique positions in the master table
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SYMBOL</th>
      <th>seqnames</th>
      <th>start</th>
      <th>end</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>79</th>
      <td>MAPK1</td>
      <td>22</td>
      <td>22160176</td>
      <td>22160176</td>
    </tr>
    <tr>
      <th>88</th>
      <td>NOTCH2</td>
      <td>1</td>
      <td>120457988</td>
      <td>120457988</td>
    </tr>
    <tr>
      <th>257</th>
      <td>LRP1B</td>
      <td>2</td>
      <td>141526827</td>
      <td>141526827</td>
    </tr>
    <tr>
      <th>328</th>
      <td>KIT</td>
      <td>4</td>
      <td>55602705</td>
      <td>55602705</td>
    </tr>
    <tr>
      <th>344</th>
      <td>MAP3K1</td>
      <td>5</td>
      <td>56180572</td>
      <td>56180572</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>24508</th>
      <td>TP53</td>
      <td>17</td>
      <td>7577090</td>
      <td>7577090</td>
    </tr>
    <tr>
      <th>36363</th>
      <td>TP53</td>
      <td>17</td>
      <td>7577535</td>
      <td>7577535</td>
    </tr>
    <tr>
      <th>39227</th>
      <td>CREBBP</td>
      <td>16</td>
      <td>3779497</td>
      <td>3779497</td>
    </tr>
    <tr>
      <th>42529</th>
      <td>KRAS</td>
      <td>12</td>
      <td>25378561</td>
      <td>25378561</td>
    </tr>
    <tr>
      <th>63968</th>
      <td>TP63</td>
      <td>3</td>
      <td>189456528</td>
      <td>189456528</td>
    </tr>
  </tbody>
</table>
<p>1068 rows × 4 columns</p>
</div>




```python
#Select required columns from whole mutation table
colon_mutation = colon_mutation_data[["SYMBOL","seqnames","start","end", "SampleID"]]
colon_mutation
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SYMBOL</th>
      <th>seqnames</th>
      <th>start</th>
      <th>end</th>
      <th>SampleID</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>SPATA21</td>
      <td>1</td>
      <td>16736303</td>
      <td>16736303</td>
      <td>eAPD114</td>
    </tr>
    <tr>
      <th>1</th>
      <td>E2F2</td>
      <td>1</td>
      <td>23836607</td>
      <td>23836607</td>
      <td>eAPD114</td>
    </tr>
    <tr>
      <th>2</th>
      <td>FCN3</td>
      <td>1</td>
      <td>27701288</td>
      <td>27701288</td>
      <td>eAPD114</td>
    </tr>
    <tr>
      <th>3</th>
      <td>MARCKSL1</td>
      <td>1</td>
      <td>32800671</td>
      <td>32800671</td>
      <td>eAPD114</td>
    </tr>
    <tr>
      <th>4</th>
      <td>LRRC40</td>
      <td>1</td>
      <td>70644607</td>
      <td>70644607</td>
      <td>eAPD114</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>73389</th>
      <td>KREMEN1</td>
      <td>22</td>
      <td>29536275</td>
      <td>29536275</td>
      <td>eAPD081</td>
    </tr>
    <tr>
      <th>73390</th>
      <td>KIF14</td>
      <td>1</td>
      <td>200569584</td>
      <td>200569584</td>
      <td>eAPD081</td>
    </tr>
    <tr>
      <th>73391</th>
      <td>RGS7BP</td>
      <td>5</td>
      <td>63802465</td>
      <td>63802465</td>
      <td>eAPD081</td>
    </tr>
    <tr>
      <th>73392</th>
      <td>PCDHB6</td>
      <td>5</td>
      <td>140531231</td>
      <td>140531231</td>
      <td>eAPD081</td>
    </tr>
    <tr>
      <th>73393</th>
      <td>SERPINB4</td>
      <td>18</td>
      <td>61305310</td>
      <td>61305310</td>
      <td>eAPD081</td>
    </tr>
  </tbody>
</table>
<p>73394 rows × 5 columns</p>
</div>




```python
#Map the all colon mutation to master table to create the matrix
cols = ['SYMBOL','seqnames','start','end']
df = master_pos_sel.merge(colon_mutation, on=cols, how='left')

df = (df.join(pd.get_dummies(df.pop('SampleID')))
        .groupby(cols).max()
        .reindex(colon_mutation['SampleID'].unique(), axis=1, fill_value=0)
        .reset_index())

df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SYMBOL</th>
      <th>seqnames</th>
      <th>start</th>
      <th>end</th>
      <th>eAPD114</th>
      <th>eAPD304</th>
      <th>eAPD286</th>
      <th>APD202</th>
      <th>APD241</th>
      <th>eAPD293</th>
      <th>...</th>
      <th>APD022</th>
      <th>APD020</th>
      <th>APD057</th>
      <th>APD024</th>
      <th>APD082</th>
      <th>APD066</th>
      <th>APD016</th>
      <th>APD006</th>
      <th>eAPD079</th>
      <th>eAPD081</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ACSL3</td>
      <td>2</td>
      <td>223773696</td>
      <td>223773696</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ACVR1</td>
      <td>2</td>
      <td>158622511</td>
      <td>158622511</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ACVR2A</td>
      <td>2</td>
      <td>148676149</td>
      <td>148676149</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>AFF4</td>
      <td>5</td>
      <td>132223637</td>
      <td>132223637</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>AFF4</td>
      <td>5</td>
      <td>132233971</td>
      <td>132233971</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1063</th>
      <td>ZNF429</td>
      <td>19</td>
      <td>21719921</td>
      <td>21719921</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1064</th>
      <td>ZNF429</td>
      <td>19</td>
      <td>21720714</td>
      <td>21720714</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1065</th>
      <td>ZNF479</td>
      <td>7</td>
      <td>57194377</td>
      <td>57194377</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1066</th>
      <td>ZNF521</td>
      <td>18</td>
      <td>22804995</td>
      <td>22804995</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1067</th>
      <td>ZNF521</td>
      <td>18</td>
      <td>22807395</td>
      <td>22807395</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>1068 rows × 205 columns</p>
</div>




```python
df.to_csv('cgc_deleterious_matrix.txt', sep='\t', index=False)
```


```python

```


```python

```


```python

```


```python

```