```python
#import the packages
import pandas as pd
import numpy as np
import os
import glob
```


```python
#Read the combined the data
colon_mutation = pd.read_table("combined_hm_t1_t2_vcf.tab", sep='\t')
```


```python
colon_mutation
```

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
      <th>SYMBOL</th>
      <th>HGVSc</th>
      <th>HGVSp</th>
      <th>CLIN_SIG</th>
      <th>PolyPhen</th>
      <th>SIFT</th>
      <th>SampleID</th>
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
      <td>SPATA21</td>
      <td>ENST00000335496.1:c.380T&gt;C</td>
      <td>ENSP00000335612.1:p.Leu127Pro</td>
      <td>NaN</td>
      <td>possibly_damaging(0.894)</td>
      <td>deleterious(0)</td>
      <td>eAPD114</td>
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
      <td>E2F2</td>
      <td>ENST00000361729.2:c.1079C&gt;T</td>
      <td>ENSP00000355249.2:p.Pro360Leu</td>
      <td>NaN</td>
      <td>benign(0)</td>
      <td>tolerated(0.48)</td>
      <td>eAPD114</td>
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
      <td>FCN3</td>
      <td>ENST00000270879.4:c.22C&gt;T</td>
      <td>ENSP00000270879.4:p.Pro8Ser</td>
      <td>NaN</td>
      <td>benign(0)</td>
      <td>tolerated(0.2)</td>
      <td>eAPD114</td>
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
      <td>MARCKSL1</td>
      <td>ENST00000329421.7:c.115G&gt;A</td>
      <td>ENSP00000362638.4:p.Asp39Asn</td>
      <td>NaN</td>
      <td>probably_damaging(1)</td>
      <td>deleterious(0.04)</td>
      <td>eAPD114</td>
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
      <td>LRRC40</td>
      <td>ENST00000370952.3:c.731C&gt;T</td>
      <td>ENSP00000359990.3:p.Ser244Leu</td>
      <td>NaN</td>
      <td>possibly_damaging(0.831)</td>
      <td>deleterious(0.01)</td>
      <td>eAPD114</td>
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
      <td>KREMEN1</td>
      <td>ENST00000327813.5:c.1180A&gt;G</td>
      <td>ENSP00000331242.5:p.Thr394Ala</td>
      <td>NaN</td>
      <td>probably_damaging(0.994)</td>
      <td>deleterious_low_confidence(0.01)</td>
      <td>eAPD081</td>
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
      <td>KIF14</td>
      <td>ENST00000367350.4:c.2200C&gt;T</td>
      <td>ENSP00000356319.4:p.Arg734Trp</td>
      <td>NaN</td>
      <td>possibly_damaging(0.517)</td>
      <td>tolerated(0.12)</td>
      <td>eAPD081</td>
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
      <td>RGS7BP</td>
      <td>ENST00000334025.2:c.14C&gt;T</td>
      <td>ENSP00000334851.2:p.Pro5Leu</td>
      <td>NaN</td>
      <td>benign(0.039)</td>
      <td>tolerated_low_confidence(0.07)</td>
      <td>eAPD081</td>
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
      <td>PCDHB6</td>
      <td>ENST00000231136.1:c.1393G&gt;A</td>
      <td>ENSP00000231136.1:p.Ala465Thr</td>
      <td>NaN</td>
      <td>probably_damaging(0.996)</td>
      <td>deleterious_low_confidence(0)</td>
      <td>eAPD081</td>
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
      <td>SERPINB4</td>
      <td>ENST00000341074.5:c.816G&gt;T</td>
      <td>ENSP00000343445.5:p.Leu272Phe</td>
      <td>NaN</td>
      <td>benign(0.411)</td>
      <td>deleterious(0.02)</td>
      <td>eAPD081</td>
    </tr>
  </tbody>
</table>
<p>73394 rows × 17 columns</p>
</div>




```python
#View type of mutation and and counts
colon_mutation['Consequence'].value_counts()
```




    missense_variant                                                                                           62153
    stop_gained                                                                                                 3627
    frameshift_variant                                                                                          2865
    missense_variant&splice_region_variant                                                                      1742
    splice_donor_variant                                                                                         983
    splice_acceptor_variant                                                                                      640
    inframe_deletion                                                                                             536
    stop_gained&splice_region_variant                                                                            135
    splice_acceptor_variant&coding_sequence_variant&intron_variant                                                99
    splice_donor_variant&coding_sequence_variant&intron_variant                                                   88
    missense_variant&NMD_transcript_variant                                                                       82
    frameshift_variant&splice_region_variant                                                                      64
    start_lost                                                                                                    58
    stop_lost                                                                                                     47
    inframe_insertion                                                                                             45
    splice_acceptor_variant&intron_variant                                                                        24
    splice_acceptor_variant&coding_sequence_variant                                                               22
    stop_lost&3_prime_UTR_variant                                                                                 20
    splice_donor_variant&coding_sequence_variant                                                                  20
    stop_gained&frameshift_variant                                                                                20
    splice_acceptor_variant&non_coding_transcript_variant                                                         19
    inframe_deletion&splice_region_variant                                                                        17
    splice_donor_variant&non_coding_transcript_variant                                                            16
    splice_donor_variant&intron_variant                                                                           12
    frameshift_variant&stop_lost                                                                                   9
    stop_gained&inframe_deletion                                                                                   6
    start_lost&5_prime_UTR_variant                                                                                 4
    stop_gained&NMD_transcript_variant                                                                             4
    splice_acceptor_variant&NMD_transcript_variant                                                                 4
    protein_altering_variant                                                                                       3
    frameshift_variant&start_lost&start_retained_variant                                                           3
    frameshift_variant&NMD_transcript_variant                                                                      3
    start_lost&splice_region_variant                                                                               3
    splice_donor_variant&non_coding_transcript_exon_variant&intron_variant                                         2
    frameshift_variant&stop_retained_variant                                                                       2
    splice_acceptor_variant&coding_sequence_variant&3_prime_UTR_variant&intron_variant                             2
    splice_donor_variant&splice_acceptor_variant&coding_sequence_variant&intron_variant                            1
    stop_gained&frameshift_variant&splice_region_variant                                                           1
    splice_acceptor_variant&3_prime_UTR_variant&intron_variant                                                     1
    inframe_deletion&NMD_transcript_variant                                                                        1
    splice_acceptor_variant&non_coding_transcript_exon_variant&intron_variant                                      1
    start_lost&inframe_deletion                                                                                    1
    stop_gained&protein_altering_variant&splice_region_variant                                                     1
    stop_gained&protein_altering_variant                                                                           1
    splice_donor_variant&splice_acceptor_variant&coding_sequence_variant&5_prime_UTR_variant&intron_variant        1
    splice_donor_variant&coding_sequence_variant&5_prime_UTR_variant&intron_variant                                1
    splice_donor_variant&intron_variant&non_coding_transcript_variant                                              1
    splice_donor_variant&NMD_transcript_variant                                                                    1
    splice_acceptor_variant&splice_donor_variant&coding_sequence_variant&intron_variant                            1
    start_lost&start_retained_variant&5_prime_UTR_variant                                                          1
    splice_donor_variant&splice_acceptor_variant&frameshift_variant&intron_variant                                 1
    Name: Consequence, dtype: int64




```python
#Replace the multiple terms with single term with higher priority of pathogenicity
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_donor_variant&conservative_inframe_deletion&splice_region_variant&intron_variant','inframe_deletion')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('missense_variant&splice_region_variant', 'missense_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('stop_gained&splice_region_variant', 'stop_gained')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_acceptor_variant&coding_sequence_variant&intron_variant', 'splice_acceptor_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_donor_variant&coding_sequence_variant&intron_variant', 'splice_donor_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('missense_variant&NMD_transcript_variant', 'missense_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('frameshift_variant&splice_region_variant', 'frameshift_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_acceptor_variant&intron_variant', 'splice_acceptor_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_acceptor_variant&coding_sequence_variant', 'splice_acceptor_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_donor_variant&coding_sequence_variant', 'splice_donor_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('stop_lost&3_prime_UTR_variant', 'stop_lost')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('stop_gained&frameshift_variant', 'frameshift_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_acceptor_variant&non_coding_transcript_variant', 'splice_acceptor_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('inframe_deletion&splice_region_variant', 'inframe_deletion')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_donor_variant&non_coding_transcript_variant', 'splice_donor_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_donor_variant&intron_variant', 'splice_donor_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('frameshift_variant&stop_lost', 'frameshift_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('stop_gained&inframe_deletion', 'stop_gained')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_acceptor_variant&NMD_transcript_variant', 'splice_acceptor_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('start_lost&5_prime_UTR_variant', 'start_lost')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('stop_gained&NMD_transcript_variant', 'stop_gained')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('start_lost&splice_region_variant', 'start_lost')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('frameshift_variant&start_lost&start_retained_variant', 'frameshift_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('frameshift_variant&NMD_transcript_variant', 'frameshift_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('frameshift_variant&stop_retained_variant', 'frameshift_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_donor_variant&non_coding_transcript_exon_variant&intron_variant', 'splice_donor_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_acceptor_variant&coding_sequence_variant&3_prime_UTR_variant&intron_variant', 'splice_acceptor_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_acceptor_variant&3_prime_UTR_variant&intron_variant', 'splice_acceptor_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('stop_gained&frameshift_variant&splice_region_variant', 'frameshift_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_donor_variant&intron_variant&non_coding_transcript_variant', 'splice_donor_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_donor_variant&splice_acceptor_variant&frameshift_variant&intron_variant', 'frameshift_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('stop_gained&protein_altering_variant', 'stop_gained')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_acceptor_variant&non_coding_transcript_exon_variant&intron_variant', 'splice_acceptor_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_donor_variant&splice_acceptor_variant&coding_sequence_variant&intron_variant', 'splice_acceptor_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('start_lost&start_retained_variant&5_prime_UTR_variant', 'start_lost')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('inframe_deletion&NMD_transcript_variant', 'inframe_deletion')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_acceptor_variant&splice_donor_variant&coding_sequence_variant&intron_variant', 'splice_acceptor_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('start_lost&inframe_deletion', 'start_lost')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_donor_variant&splice_acceptor_variant&coding_sequence_variant&5_prime_UTR_variant&intron_variant', 'splice_acceptor_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_donor_variant&coding_sequence_variant&5_prime_UTR_variant&intron_variant', 'splice_donor_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('stop_gained&protein_altering_variant&splice_region_variant', 'stop_gained')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_donor_variant&NMD_transcript_variant', 'splice_donor_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_donor_variant&5_prime_UTR_variant&intron_variant','splice_donor_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_donor_variant&splice_acceptor_variant&5_prime_UTR_variant&intron_variant', 'splice_acceptor_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_donor_variant&splice_acceptor_variant', 'splice_acceptor_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_acceptor_variant&splice_donor_variant', 'splice_acceptor_variant')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('stop_gained&splice_region_variant', 'stop_gained')
colon_mutation['Consequence']=colon_mutation['Consequence'].str.replace('splice_donor_variant&non_coding_transcript_variant', 'splice_donor_variant')

```


```python
#Unified variants
colon_mutation['Consequence'].value_counts()
```




    missense_variant            63977
    stop_gained                  3774
    frameshift_variant           2968
    splice_donor_variant         1124
    splice_acceptor_variant       815
    inframe_deletion              554
    stop_lost                      67
    start_lost                     67
    inframe_insertion              45
    protein_altering_variant        3
    Name: Consequence, dtype: int64




```python
#Clinical terms in clinvar
colon_mutation['CLIN_SIG'].value_counts()
```




    benign                                                                       902
    likely_benign                                                                421
    uncertain_significance                                                       399
    pathogenic                                                                   157
    benign&likely_benign                                                         105
                                                                                ... 
    pathogenic&risk_factor&likely_benign                                           1
    benign&likely_benign&benign/likely_benign                                      1
    drug_response&not_provided&pathogenic                                          1
    uncertain_significance&pathogenic&benign/likely_benign                         1
    conflicting_interpretations_of_pathogenicity&pathogenic&likely_pathogenic      1
    Name: CLIN_SIG, Length: 92, dtype: int64




```python
#Splitiing polyphen score
colon_mutation[['POLYPHEN','POLYSCORE']] = colon_mutation.PolyPhen.str.split('\(|\)', expand=True).iloc[:,[0,1]]
```


```python
#Splitiing SIFT score
colon_mutation[['SIFTS','SIFTSCORE']] = colon_mutation.SIFT.str.split('\(|\)', expand=True).iloc[:,[0,1]]
```


```python
#View the table with splitted score of polyphen and sift
colon_mutation
```

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
      <td>0</td>
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
      <td>0</td>
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
      <td>0</td>
      <td>tolerated</td>
      <td>0.2</td>
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
      <td>1</td>
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
      <td>0</td>
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
#Create local copy for the file
colon_mutation.to_csv('colon_mutation_poly_sift_score.txt', sep="\t", index=False)
```


```python
#Checking the pathogenic data reported by Clinvar
colon_mutation_clinvar = colon_mutation[colon_mutation['CLIN_SIG'].str.contains("pathogenic", na=False)]
colon_mutation_clinvar

#there are 411 pathogenic clinvar variants
```
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
      <th>54</th>
      <td>16</td>
      <td>16263524</td>
      <td>16263524</td>
      <td>1</td>
      <td>*</td>
      <td>15</td>
      <td>3</td>
      <td>0.167</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENST00000205557.7:c.2974G&gt;A</td>
      <td>ENSP00000205557.7:p.Gly992Arg</td>
      <td>pathogenic</td>
      <td>probably_damaging(0.968)</td>
      <td>deleterious(0)</td>
      <td>eAPD114</td>
      <td>probably_damaging</td>
      <td>0.968</td>
      <td>deleterious</td>
      <td>0</td>
    </tr>
    <tr>
      <th>410</th>
      <td>7</td>
      <td>117149143</td>
      <td>117149143</td>
      <td>1</td>
      <td>*</td>
      <td>22</td>
      <td>6</td>
      <td>0.214</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENST00000003084.6:c.220C&gt;T</td>
      <td>ENSP00000003084.6:p.Arg74Trp</td>
      <td>drug_response&amp;conflicting_interpretations_of_p...</td>
      <td>possibly_damaging(0.677)</td>
      <td>tolerated(0.19)</td>
      <td>eAPD304</td>
      <td>possibly_damaging</td>
      <td>0.677</td>
      <td>tolerated</td>
      <td>0.19</td>
    </tr>
    <tr>
      <th>540</th>
      <td>13</td>
      <td>110830279</td>
      <td>110830279</td>
      <td>1</td>
      <td>*</td>
      <td>20</td>
      <td>3</td>
      <td>0.130</td>
      <td>splice_acceptor_variant</td>
      <td>HIGH</td>
      <td>...</td>
      <td>ENST00000375820.4:c.2627-1G&gt;A</td>
      <td>NaN</td>
      <td>likely_pathogenic</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>eAPD304</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1482</th>
      <td>11</td>
      <td>63988121</td>
      <td>63988121</td>
      <td>1</td>
      <td>*</td>
      <td>15</td>
      <td>4</td>
      <td>0.238</td>
      <td>stop_gained</td>
      <td>HIGH</td>
      <td>...</td>
      <td>ENST00000279227.5:c.1537C&gt;T</td>
      <td>ENSP00000279227.5:p.Arg513Ter</td>
      <td>pathogenic</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>eAPD286</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1543</th>
      <td>17</td>
      <td>7579358</td>
      <td>7579358</td>
      <td>1</td>
      <td>*</td>
      <td>9</td>
      <td>7</td>
      <td>0.444</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENST00000269305.4:c.329G&gt;C</td>
      <td>ENSP00000269305.4:p.Arg110Pro</td>
      <td>likely_pathogenic&amp;pathogenic</td>
      <td>possibly_damaging(0.878)</td>
      <td>deleterious(0.03)</td>
      <td>eAPD286</td>
      <td>possibly_damaging</td>
      <td>0.878</td>
      <td>deleterious</td>
      <td>0.03</td>
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
      <th>72690</th>
      <td>13</td>
      <td>41373319</td>
      <td>41373319</td>
      <td>1</td>
      <td>*</td>
      <td>48</td>
      <td>43</td>
      <td>0.473</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENST00000338625.4:c.182G&gt;A</td>
      <td>ENSP00000342267.4:p.Arg61His</td>
      <td>conflicting_interpretations_of_pathogenicity</td>
      <td>benign(0.052)</td>
      <td>tolerated(0.05)</td>
      <td>APD066</td>
      <td>benign</td>
      <td>0.052</td>
      <td>tolerated</td>
      <td>0.05</td>
    </tr>
    <tr>
      <th>73223</th>
      <td>3</td>
      <td>178916930</td>
      <td>178916930</td>
      <td>1</td>
      <td>*</td>
      <td>19</td>
      <td>4</td>
      <td>0.174</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENST00000263967.3:c.317G&gt;T</td>
      <td>ENSP00000263967.3:p.Gly106Val</td>
      <td>uncertain_significance&amp;likely_pathogenic</td>
      <td>probably_damaging(1)</td>
      <td>deleterious(0.01)</td>
      <td>APD006</td>
      <td>probably_damaging</td>
      <td>1</td>
      <td>deleterious</td>
      <td>0.01</td>
    </tr>
    <tr>
      <th>73244</th>
      <td>12</td>
      <td>25398284</td>
      <td>25398284</td>
      <td>1</td>
      <td>*</td>
      <td>37</td>
      <td>11</td>
      <td>0.229</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>...</td>
      <td>ENST00000256078.4:c.35G&gt;A</td>
      <td>ENSP00000256078.4:p.Gly12Asp</td>
      <td>pathogenic&amp;likely_pathogenic</td>
      <td>benign(0.303)</td>
      <td>deleterious(0)</td>
      <td>APD006</td>
      <td>benign</td>
      <td>0.303</td>
      <td>deleterious</td>
      <td>0</td>
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
      <td>ENST00000256078.4:c.35G&gt;T</td>
      <td>ENSP00000256078.4:p.Gly12Val</td>
      <td>pathogenic&amp;pathogenic/likely_pathogenic&amp;likely...</td>
      <td>probably_damaging(0.972)</td>
      <td>deleterious(0)</td>
      <td>eAPD079</td>
      <td>probably_damaging</td>
      <td>0.972</td>
      <td>deleterious</td>
      <td>0</td>
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
      <td>ENST00000269305.4:c.586C&gt;T</td>
      <td>ENSP00000269305.4:p.Arg196Ter</td>
      <td>pathogenic</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>eAPD079</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>411 rows × 21 columns</p>
</div>




```python
#drop repeated columns
colon_mutation_clinvar.drop(['PolyPhen', 'SIFT'], axis=1, inplace=True)
colon_mutation_clinvar
```

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
      <th>SYMBOL</th>
      <th>HGVSc</th>
      <th>HGVSp</th>
      <th>CLIN_SIG</th>
      <th>SampleID</th>
      <th>POLYPHEN</th>
      <th>POLYSCORE</th>
      <th>SIFTS</th>
      <th>SIFTSCORE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>54</th>
      <td>16</td>
      <td>16263524</td>
      <td>16263524</td>
      <td>1</td>
      <td>*</td>
      <td>15</td>
      <td>3</td>
      <td>0.167</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>ABCC6</td>
      <td>ENST00000205557.7:c.2974G&gt;A</td>
      <td>ENSP00000205557.7:p.Gly992Arg</td>
      <td>pathogenic</td>
      <td>eAPD114</td>
      <td>probably_damaging</td>
      <td>0.968</td>
      <td>deleterious</td>
      <td>0</td>
    </tr>
    <tr>
      <th>410</th>
      <td>7</td>
      <td>117149143</td>
      <td>117149143</td>
      <td>1</td>
      <td>*</td>
      <td>22</td>
      <td>6</td>
      <td>0.214</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>CFTR</td>
      <td>ENST00000003084.6:c.220C&gt;T</td>
      <td>ENSP00000003084.6:p.Arg74Trp</td>
      <td>drug_response&amp;conflicting_interpretations_of_p...</td>
      <td>eAPD304</td>
      <td>possibly_damaging</td>
      <td>0.677</td>
      <td>tolerated</td>
      <td>0.19</td>
    </tr>
    <tr>
      <th>540</th>
      <td>13</td>
      <td>110830279</td>
      <td>110830279</td>
      <td>1</td>
      <td>*</td>
      <td>20</td>
      <td>3</td>
      <td>0.130</td>
      <td>splice_acceptor_variant</td>
      <td>HIGH</td>
      <td>COL4A1</td>
      <td>ENST00000375820.4:c.2627-1G&gt;A</td>
      <td>NaN</td>
      <td>likely_pathogenic</td>
      <td>eAPD304</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1482</th>
      <td>11</td>
      <td>63988121</td>
      <td>63988121</td>
      <td>1</td>
      <td>*</td>
      <td>15</td>
      <td>4</td>
      <td>0.238</td>
      <td>stop_gained</td>
      <td>HIGH</td>
      <td>FERMT3</td>
      <td>ENST00000279227.5:c.1537C&gt;T</td>
      <td>ENSP00000279227.5:p.Arg513Ter</td>
      <td>pathogenic</td>
      <td>eAPD286</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1543</th>
      <td>17</td>
      <td>7579358</td>
      <td>7579358</td>
      <td>1</td>
      <td>*</td>
      <td>9</td>
      <td>7</td>
      <td>0.444</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>TP53</td>
      <td>ENST00000269305.4:c.329G&gt;C</td>
      <td>ENSP00000269305.4:p.Arg110Pro</td>
      <td>likely_pathogenic&amp;pathogenic</td>
      <td>eAPD286</td>
      <td>possibly_damaging</td>
      <td>0.878</td>
      <td>deleterious</td>
      <td>0.03</td>
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
    </tr>
    <tr>
      <th>72690</th>
      <td>13</td>
      <td>41373319</td>
      <td>41373319</td>
      <td>1</td>
      <td>*</td>
      <td>48</td>
      <td>43</td>
      <td>0.473</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>SLC25A15</td>
      <td>ENST00000338625.4:c.182G&gt;A</td>
      <td>ENSP00000342267.4:p.Arg61His</td>
      <td>conflicting_interpretations_of_pathogenicity</td>
      <td>APD066</td>
      <td>benign</td>
      <td>0.052</td>
      <td>tolerated</td>
      <td>0.05</td>
    </tr>
    <tr>
      <th>73223</th>
      <td>3</td>
      <td>178916930</td>
      <td>178916930</td>
      <td>1</td>
      <td>*</td>
      <td>19</td>
      <td>4</td>
      <td>0.174</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>PIK3CA</td>
      <td>ENST00000263967.3:c.317G&gt;T</td>
      <td>ENSP00000263967.3:p.Gly106Val</td>
      <td>uncertain_significance&amp;likely_pathogenic</td>
      <td>APD006</td>
      <td>probably_damaging</td>
      <td>1</td>
      <td>deleterious</td>
      <td>0.01</td>
    </tr>
    <tr>
      <th>73244</th>
      <td>12</td>
      <td>25398284</td>
      <td>25398284</td>
      <td>1</td>
      <td>*</td>
      <td>37</td>
      <td>11</td>
      <td>0.229</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>KRAS</td>
      <td>ENST00000256078.4:c.35G&gt;A</td>
      <td>ENSP00000256078.4:p.Gly12Asp</td>
      <td>pathogenic&amp;likely_pathogenic</td>
      <td>APD006</td>
      <td>benign</td>
      <td>0.303</td>
      <td>deleterious</td>
      <td>0</td>
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
      <td>KRAS</td>
      <td>ENST00000256078.4:c.35G&gt;T</td>
      <td>ENSP00000256078.4:p.Gly12Val</td>
      <td>pathogenic&amp;pathogenic/likely_pathogenic&amp;likely...</td>
      <td>eAPD079</td>
      <td>probably_damaging</td>
      <td>0.972</td>
      <td>deleterious</td>
      <td>0</td>
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
      <td>TP53</td>
      <td>ENST00000269305.4:c.586C&gt;T</td>
      <td>ENSP00000269305.4:p.Arg196Ter</td>
      <td>pathogenic</td>
      <td>eAPD079</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>411 rows × 19 columns</p>
</div>




```python
#count annotation terms of polyphen in clnvar
colon_mutation_clinvar['POLYPHEN'].value_counts()
```




    probably_damaging    172
    benign                94
    possibly_damaging     56
    Name: POLYPHEN, dtype: int64




```python
##count annotation terms of polyphen in clnvar
colon_mutation_clinvar['SIFTS'].value_counts()
```




    deleterious                   247
    tolerated                      71
    deleterious_low_confidence      3
    tolerated_low_confidence        1
    Name: SIFTS, dtype: int64




```python
colon_mutation_clinvar2 = colon_mutation_clinvar.copy() #make a local copy
```


```python
#replace non-pathogenic values of polyphen with 0
colon_clin_poly=colon_mutation_clinvar.replace(to_replace =["benign", "possibly_damaging","unknown"], 
                            value =0)

##replace pathogenic values of polyphen with 1
colon_clin_poly=colon_clin_poly.replace(to_replace =["probably_damaging"], 
                            value =1)
#view the update
colon_clin_poly
```


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
      <th>SYMBOL</th>
      <th>HGVSc</th>
      <th>HGVSp</th>
      <th>CLIN_SIG</th>
      <th>SampleID</th>
      <th>POLYPHEN</th>
      <th>POLYSCORE</th>
      <th>SIFTS</th>
      <th>SIFTSCORE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>54</th>
      <td>16</td>
      <td>16263524</td>
      <td>16263524</td>
      <td>1</td>
      <td>*</td>
      <td>15</td>
      <td>3</td>
      <td>0.167</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>ABCC6</td>
      <td>ENST00000205557.7:c.2974G&gt;A</td>
      <td>ENSP00000205557.7:p.Gly992Arg</td>
      <td>pathogenic</td>
      <td>eAPD114</td>
      <td>1.0</td>
      <td>0.968</td>
      <td>deleterious</td>
      <td>0</td>
    </tr>
    <tr>
      <th>410</th>
      <td>7</td>
      <td>117149143</td>
      <td>117149143</td>
      <td>1</td>
      <td>*</td>
      <td>22</td>
      <td>6</td>
      <td>0.214</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>CFTR</td>
      <td>ENST00000003084.6:c.220C&gt;T</td>
      <td>ENSP00000003084.6:p.Arg74Trp</td>
      <td>drug_response&amp;conflicting_interpretations_of_p...</td>
      <td>eAPD304</td>
      <td>0.0</td>
      <td>0.677</td>
      <td>tolerated</td>
      <td>0.19</td>
    </tr>
    <tr>
      <th>540</th>
      <td>13</td>
      <td>110830279</td>
      <td>110830279</td>
      <td>1</td>
      <td>*</td>
      <td>20</td>
      <td>3</td>
      <td>0.130</td>
      <td>splice_acceptor_variant</td>
      <td>HIGH</td>
      <td>COL4A1</td>
      <td>ENST00000375820.4:c.2627-1G&gt;A</td>
      <td>NaN</td>
      <td>likely_pathogenic</td>
      <td>eAPD304</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1482</th>
      <td>11</td>
      <td>63988121</td>
      <td>63988121</td>
      <td>1</td>
      <td>*</td>
      <td>15</td>
      <td>4</td>
      <td>0.238</td>
      <td>stop_gained</td>
      <td>HIGH</td>
      <td>FERMT3</td>
      <td>ENST00000279227.5:c.1537C&gt;T</td>
      <td>ENSP00000279227.5:p.Arg513Ter</td>
      <td>pathogenic</td>
      <td>eAPD286</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1543</th>
      <td>17</td>
      <td>7579358</td>
      <td>7579358</td>
      <td>1</td>
      <td>*</td>
      <td>9</td>
      <td>7</td>
      <td>0.444</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>TP53</td>
      <td>ENST00000269305.4:c.329G&gt;C</td>
      <td>ENSP00000269305.4:p.Arg110Pro</td>
      <td>likely_pathogenic&amp;pathogenic</td>
      <td>eAPD286</td>
      <td>0.0</td>
      <td>0.878</td>
      <td>deleterious</td>
      <td>0.03</td>
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
    </tr>
    <tr>
      <th>72690</th>
      <td>13</td>
      <td>41373319</td>
      <td>41373319</td>
      <td>1</td>
      <td>*</td>
      <td>48</td>
      <td>43</td>
      <td>0.473</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>SLC25A15</td>
      <td>ENST00000338625.4:c.182G&gt;A</td>
      <td>ENSP00000342267.4:p.Arg61His</td>
      <td>conflicting_interpretations_of_pathogenicity</td>
      <td>APD066</td>
      <td>0.0</td>
      <td>0.052</td>
      <td>tolerated</td>
      <td>0.05</td>
    </tr>
    <tr>
      <th>73223</th>
      <td>3</td>
      <td>178916930</td>
      <td>178916930</td>
      <td>1</td>
      <td>*</td>
      <td>19</td>
      <td>4</td>
      <td>0.174</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>PIK3CA</td>
      <td>ENST00000263967.3:c.317G&gt;T</td>
      <td>ENSP00000263967.3:p.Gly106Val</td>
      <td>uncertain_significance&amp;likely_pathogenic</td>
      <td>APD006</td>
      <td>1.0</td>
      <td>1</td>
      <td>deleterious</td>
      <td>0.01</td>
    </tr>
    <tr>
      <th>73244</th>
      <td>12</td>
      <td>25398284</td>
      <td>25398284</td>
      <td>1</td>
      <td>*</td>
      <td>37</td>
      <td>11</td>
      <td>0.229</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>KRAS</td>
      <td>ENST00000256078.4:c.35G&gt;A</td>
      <td>ENSP00000256078.4:p.Gly12Asp</td>
      <td>pathogenic&amp;likely_pathogenic</td>
      <td>APD006</td>
      <td>0.0</td>
      <td>0.303</td>
      <td>deleterious</td>
      <td>0</td>
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
      <td>KRAS</td>
      <td>ENST00000256078.4:c.35G&gt;T</td>
      <td>ENSP00000256078.4:p.Gly12Val</td>
      <td>pathogenic&amp;pathogenic/likely_pathogenic&amp;likely...</td>
      <td>eAPD079</td>
      <td>1.0</td>
      <td>0.972</td>
      <td>deleterious</td>
      <td>0</td>
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
      <td>TP53</td>
      <td>ENST00000269305.4:c.586C&gt;T</td>
      <td>ENSP00000269305.4:p.Arg196Ter</td>
      <td>pathogenic</td>
      <td>eAPD079</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>411 rows × 19 columns</p>
</div>




```python
#Get the count of 0 and 1 in polyphen
colon_clin_poly['POLYPHEN'].value_counts()
```




    1.0    172
    0.0    150
    Name: POLYPHEN, dtype: int64




```python
#replace non-pathogenic values of SIFT with 0
colon_clin_poly_sift=colon_clin_poly.replace(to_replace =["tolerated", "deleterious_low_confidence","tolerated_low_confidence"], 
                            value =0)

##replace pathogenic values of SIFT with 1
colon_clin_poly_sift=colon_clin_poly_sift.replace(to_replace =["deleterious"], 
                            value =1)
#View the updates
colon_clin_poly_sift
```


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
      <th>SYMBOL</th>
      <th>HGVSc</th>
      <th>HGVSp</th>
      <th>CLIN_SIG</th>
      <th>SampleID</th>
      <th>POLYPHEN</th>
      <th>POLYSCORE</th>
      <th>SIFTS</th>
      <th>SIFTSCORE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>54</th>
      <td>16</td>
      <td>16263524</td>
      <td>16263524</td>
      <td>1</td>
      <td>*</td>
      <td>15</td>
      <td>3</td>
      <td>0.167</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>ABCC6</td>
      <td>ENST00000205557.7:c.2974G&gt;A</td>
      <td>ENSP00000205557.7:p.Gly992Arg</td>
      <td>pathogenic</td>
      <td>eAPD114</td>
      <td>1.0</td>
      <td>0.968</td>
      <td>1.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>410</th>
      <td>7</td>
      <td>117149143</td>
      <td>117149143</td>
      <td>1</td>
      <td>*</td>
      <td>22</td>
      <td>6</td>
      <td>0.214</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>CFTR</td>
      <td>ENST00000003084.6:c.220C&gt;T</td>
      <td>ENSP00000003084.6:p.Arg74Trp</td>
      <td>drug_response&amp;conflicting_interpretations_of_p...</td>
      <td>eAPD304</td>
      <td>0.0</td>
      <td>0.677</td>
      <td>0.0</td>
      <td>0.19</td>
    </tr>
    <tr>
      <th>540</th>
      <td>13</td>
      <td>110830279</td>
      <td>110830279</td>
      <td>1</td>
      <td>*</td>
      <td>20</td>
      <td>3</td>
      <td>0.130</td>
      <td>splice_acceptor_variant</td>
      <td>HIGH</td>
      <td>COL4A1</td>
      <td>ENST00000375820.4:c.2627-1G&gt;A</td>
      <td>NaN</td>
      <td>likely_pathogenic</td>
      <td>eAPD304</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1482</th>
      <td>11</td>
      <td>63988121</td>
      <td>63988121</td>
      <td>1</td>
      <td>*</td>
      <td>15</td>
      <td>4</td>
      <td>0.238</td>
      <td>stop_gained</td>
      <td>HIGH</td>
      <td>FERMT3</td>
      <td>ENST00000279227.5:c.1537C&gt;T</td>
      <td>ENSP00000279227.5:p.Arg513Ter</td>
      <td>pathogenic</td>
      <td>eAPD286</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1543</th>
      <td>17</td>
      <td>7579358</td>
      <td>7579358</td>
      <td>1</td>
      <td>*</td>
      <td>9</td>
      <td>7</td>
      <td>0.444</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>TP53</td>
      <td>ENST00000269305.4:c.329G&gt;C</td>
      <td>ENSP00000269305.4:p.Arg110Pro</td>
      <td>likely_pathogenic&amp;pathogenic</td>
      <td>eAPD286</td>
      <td>0.0</td>
      <td>0.878</td>
      <td>1.0</td>
      <td>0.03</td>
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
    </tr>
    <tr>
      <th>72690</th>
      <td>13</td>
      <td>41373319</td>
      <td>41373319</td>
      <td>1</td>
      <td>*</td>
      <td>48</td>
      <td>43</td>
      <td>0.473</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>SLC25A15</td>
      <td>ENST00000338625.4:c.182G&gt;A</td>
      <td>ENSP00000342267.4:p.Arg61His</td>
      <td>conflicting_interpretations_of_pathogenicity</td>
      <td>APD066</td>
      <td>0.0</td>
      <td>0.052</td>
      <td>0.0</td>
      <td>0.05</td>
    </tr>
    <tr>
      <th>73223</th>
      <td>3</td>
      <td>178916930</td>
      <td>178916930</td>
      <td>1</td>
      <td>*</td>
      <td>19</td>
      <td>4</td>
      <td>0.174</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>PIK3CA</td>
      <td>ENST00000263967.3:c.317G&gt;T</td>
      <td>ENSP00000263967.3:p.Gly106Val</td>
      <td>uncertain_significance&amp;likely_pathogenic</td>
      <td>APD006</td>
      <td>1.0</td>
      <td>1</td>
      <td>1.0</td>
      <td>0.01</td>
    </tr>
    <tr>
      <th>73244</th>
      <td>12</td>
      <td>25398284</td>
      <td>25398284</td>
      <td>1</td>
      <td>*</td>
      <td>37</td>
      <td>11</td>
      <td>0.229</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>KRAS</td>
      <td>ENST00000256078.4:c.35G&gt;A</td>
      <td>ENSP00000256078.4:p.Gly12Asp</td>
      <td>pathogenic&amp;likely_pathogenic</td>
      <td>APD006</td>
      <td>0.0</td>
      <td>0.303</td>
      <td>1.0</td>
      <td>0</td>
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
      <td>KRAS</td>
      <td>ENST00000256078.4:c.35G&gt;T</td>
      <td>ENSP00000256078.4:p.Gly12Val</td>
      <td>pathogenic&amp;pathogenic/likely_pathogenic&amp;likely...</td>
      <td>eAPD079</td>
      <td>1.0</td>
      <td>0.972</td>
      <td>1.0</td>
      <td>0</td>
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
      <td>TP53</td>
      <td>ENST00000269305.4:c.586C&gt;T</td>
      <td>ENSP00000269305.4:p.Arg196Ter</td>
      <td>pathogenic</td>
      <td>eAPD079</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>411 rows × 19 columns</p>
</div>




```python
#Get the count of 0 and 1 in SIFT
colon_clin_poly_sift['SIFTS'].value_counts()
```




    1.0    247
    0.0     75
    Name: SIFTS, dtype: int64




```python
#Fill empty columns of polyphen , sift and clinvar with 0
colon_clin_poly_sift['CLIN_SIG'].fillna(0, inplace=True)
colon_clin_poly_sift['POLYPHEN'].fillna(0, inplace=True)
colon_clin_poly_sift['SIFTS'].fillna(0, inplace=True)
```


```python
#columns of the dataframe
colon_clin_poly_sift.columns
```




    Index(['seqnames', 'start', 'end', 'width', 'strand', 'AD', 'AD.1', 'AF',
           'Consequence', 'IMPACT', 'SYMBOL', 'HGVSc', 'HGVSp', 'CLIN_SIG',
           'SampleID', 'POLYPHEN', 'POLYSCORE', 'SIFTS', 'SIFTSCORE'],
          dtype='object')




```python
#Consider only required columns from the dataframe
colon_clin_poly_sift_select = colon_clin_poly_sift[['SYMBOL', 'seqnames', 'start', 'end','CLIN_SIG',
                                                    'Consequence', 'IMPACT', 'SIFTS', 'POLYPHEN']]
#Create the master table by removing duplicated positions
master_tab = colon_clin_poly_sift_select.drop_duplicates()
master_tab
```


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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>54</th>
      <td>ABCC6</td>
      <td>16</td>
      <td>16263524</td>
      <td>16263524</td>
      <td>pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>410</th>
      <td>CFTR</td>
      <td>7</td>
      <td>117149143</td>
      <td>117149143</td>
      <td>drug_response&amp;conflicting_interpretations_of_p...</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>540</th>
      <td>COL4A1</td>
      <td>13</td>
      <td>110830279</td>
      <td>110830279</td>
      <td>likely_pathogenic</td>
      <td>splice_acceptor_variant</td>
      <td>HIGH</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1482</th>
      <td>FERMT3</td>
      <td>11</td>
      <td>63988121</td>
      <td>63988121</td>
      <td>pathogenic</td>
      <td>stop_gained</td>
      <td>HIGH</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1543</th>
      <td>TP53</td>
      <td>17</td>
      <td>7579358</td>
      <td>7579358</td>
      <td>likely_pathogenic&amp;pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>0.0</td>
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
    </tr>
    <tr>
      <th>72110</th>
      <td>DARC</td>
      <td>1</td>
      <td>159175494</td>
      <td>159175494</td>
      <td>pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>72461</th>
      <td>RP1</td>
      <td>8</td>
      <td>55537560</td>
      <td>55537560</td>
      <td>pathogenic&amp;likely_benign</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>72592</th>
      <td>RAPSN</td>
      <td>11</td>
      <td>47469631</td>
      <td>47469631</td>
      <td>conflicting_interpretations_of_pathogenicity&amp;p...</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>72690</th>
      <td>SLC25A15</td>
      <td>13</td>
      <td>41373319</td>
      <td>41373319</td>
      <td>conflicting_interpretations_of_pathogenicity</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>73223</th>
      <td>PIK3CA</td>
      <td>3</td>
      <td>178916930</td>
      <td>178916930</td>
      <td>uncertain_significance&amp;likely_pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
<p>287 rows × 9 columns</p>
</div>




```python
#Create a local copy of master positions
master_tab.to_csv('master_pos.txt', sep='\t', index=False)
```


```python
#SIFT Predicting the mutation as deleterious
master_tab[master_tab['SIFTS']==1]

#There are 148 master positions
```


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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>54</th>
      <td>ABCC6</td>
      <td>16</td>
      <td>16263524</td>
      <td>16263524</td>
      <td>pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1543</th>
      <td>TP53</td>
      <td>17</td>
      <td>7579358</td>
      <td>7579358</td>
      <td>likely_pathogenic&amp;pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1676</th>
      <td>KRAS</td>
      <td>12</td>
      <td>25398284</td>
      <td>25398284</td>
      <td>pathogenic&amp;likely_pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1747</th>
      <td>PIK3CA</td>
      <td>3</td>
      <td>178936091</td>
      <td>178936091</td>
      <td>not_provided&amp;pathogenic&amp;likely_pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1835</th>
      <td>PLOD1</td>
      <td>1</td>
      <td>12032953</td>
      <td>12032953</td>
      <td>uncertain_significance&amp;conflicting_interpretat...</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
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
    </tr>
    <tr>
      <th>72014</th>
      <td>ABCC6</td>
      <td>16</td>
      <td>16253412</td>
      <td>16253412</td>
      <td>pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>72038</th>
      <td>DCX</td>
      <td>X</td>
      <td>110644337</td>
      <td>110644337</td>
      <td>pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>72461</th>
      <td>RP1</td>
      <td>8</td>
      <td>55537560</td>
      <td>55537560</td>
      <td>pathogenic&amp;likely_benign</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>72592</th>
      <td>RAPSN</td>
      <td>11</td>
      <td>47469631</td>
      <td>47469631</td>
      <td>conflicting_interpretations_of_pathogenicity&amp;p...</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73223</th>
      <td>PIK3CA</td>
      <td>3</td>
      <td>178916930</td>
      <td>178916930</td>
      <td>uncertain_significance&amp;likely_pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
<p>148 rows × 9 columns</p>
</div>




```python
#polyPhen Predicting the mutation as deleterious
master_tab[master_tab['POLYPHEN']==1]

#There are 121 master positions
```

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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>54</th>
      <td>ABCC6</td>
      <td>16</td>
      <td>16263524</td>
      <td>16263524</td>
      <td>pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1747</th>
      <td>PIK3CA</td>
      <td>3</td>
      <td>178936091</td>
      <td>178936091</td>
      <td>not_provided&amp;pathogenic&amp;likely_pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1835</th>
      <td>PLOD1</td>
      <td>1</td>
      <td>12032953</td>
      <td>12032953</td>
      <td>uncertain_significance&amp;conflicting_interpretat...</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2101</th>
      <td>BRAF</td>
      <td>7</td>
      <td>140453136</td>
      <td>140453136</td>
      <td>pathogenic&amp;likely_pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4030</th>
      <td>GJC2</td>
      <td>1</td>
      <td>228346237</td>
      <td>228346237</td>
      <td>pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
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
    </tr>
    <tr>
      <th>71956</th>
      <td>PIK3CA</td>
      <td>3</td>
      <td>178916876</td>
      <td>178916876</td>
      <td>likely_pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>0.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>72014</th>
      <td>ABCC6</td>
      <td>16</td>
      <td>16253412</td>
      <td>16253412</td>
      <td>pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>72038</th>
      <td>DCX</td>
      <td>X</td>
      <td>110644337</td>
      <td>110644337</td>
      <td>pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>72592</th>
      <td>RAPSN</td>
      <td>11</td>
      <td>47469631</td>
      <td>47469631</td>
      <td>conflicting_interpretations_of_pathogenicity&amp;p...</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73223</th>
      <td>PIK3CA</td>
      <td>3</td>
      <td>178916930</td>
      <td>178916930</td>
      <td>uncertain_significance&amp;likely_pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
<p>121 rows × 9 columns</p>
</div>




```python
#sift and polypjen Predicting the mutation as deleterious
master_tab[(master_tab.SIFTS == 1) & (master_tab.POLYPHEN == 1)] 

#There are 111 master positions
```

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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>54</th>
      <td>ABCC6</td>
      <td>16</td>
      <td>16263524</td>
      <td>16263524</td>
      <td>pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1747</th>
      <td>PIK3CA</td>
      <td>3</td>
      <td>178936091</td>
      <td>178936091</td>
      <td>not_provided&amp;pathogenic&amp;likely_pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1835</th>
      <td>PLOD1</td>
      <td>1</td>
      <td>12032953</td>
      <td>12032953</td>
      <td>uncertain_significance&amp;conflicting_interpretat...</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2101</th>
      <td>BRAF</td>
      <td>7</td>
      <td>140453136</td>
      <td>140453136</td>
      <td>pathogenic&amp;likely_pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4030</th>
      <td>GJC2</td>
      <td>1</td>
      <td>228346237</td>
      <td>228346237</td>
      <td>pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
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
    </tr>
    <tr>
      <th>71897</th>
      <td>SMAD4</td>
      <td>18</td>
      <td>48604787</td>
      <td>48604787</td>
      <td>pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>72014</th>
      <td>ABCC6</td>
      <td>16</td>
      <td>16253412</td>
      <td>16253412</td>
      <td>pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>72038</th>
      <td>DCX</td>
      <td>X</td>
      <td>110644337</td>
      <td>110644337</td>
      <td>pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>72592</th>
      <td>RAPSN</td>
      <td>11</td>
      <td>47469631</td>
      <td>47469631</td>
      <td>conflicting_interpretations_of_pathogenicity&amp;p...</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>73223</th>
      <td>PIK3CA</td>
      <td>3</td>
      <td>178916930</td>
      <td>178916930</td>
      <td>uncertain_significance&amp;likely_pathogenic</td>
      <td>missense_variant</td>
      <td>MODERATE</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
<p>111 rows × 9 columns</p>
</div>




```python
#Either sift or polypjen Predicting the mutation as deleterious
master_tab[(master_tab.SIFTS == 1) | (master_tab.POLYPHEN == 1)]
```


```python
#Considered Either sift or polypjen Predicting the mutation as deleterious
master_fil = master_tab[(master_tab.SIFTS == 1) | (master_tab.POLYPHEN == 1)]
master_selected = master_fil[['SYMBOL','seqnames','start','end']]
master_selected=master_selected.drop_duplicates()
master_selected
```


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
      <th>54</th>
      <td>ABCC6</td>
      <td>16</td>
      <td>16263524</td>
      <td>16263524</td>
    </tr>
    <tr>
      <th>1543</th>
      <td>TP53</td>
      <td>17</td>
      <td>7579358</td>
      <td>7579358</td>
    </tr>
    <tr>
      <th>1676</th>
      <td>KRAS</td>
      <td>12</td>
      <td>25398284</td>
      <td>25398284</td>
    </tr>
    <tr>
      <th>1747</th>
      <td>PIK3CA</td>
      <td>3</td>
      <td>178936091</td>
      <td>178936091</td>
    </tr>
    <tr>
      <th>1835</th>
      <td>PLOD1</td>
      <td>1</td>
      <td>12032953</td>
      <td>12032953</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>72014</th>
      <td>ABCC6</td>
      <td>16</td>
      <td>16253412</td>
      <td>16253412</td>
    </tr>
    <tr>
      <th>72038</th>
      <td>DCX</td>
      <td>X</td>
      <td>110644337</td>
      <td>110644337</td>
    </tr>
    <tr>
      <th>72461</th>
      <td>RP1</td>
      <td>8</td>
      <td>55537560</td>
      <td>55537560</td>
    </tr>
    <tr>
      <th>72592</th>
      <td>RAPSN</td>
      <td>11</td>
      <td>47469631</td>
      <td>47469631</td>
    </tr>
    <tr>
      <th>73223</th>
      <td>PIK3CA</td>
      <td>3</td>
      <td>178916930</td>
      <td>178916930</td>
    </tr>
  </tbody>
</table>
<p>155 rows × 4 columns</p>
</div>



```python
#View column names of whole mutation data loaded earlier in the analysis
colon_mutation.columns
```




    Index(['seqnames', 'start', 'end', 'width', 'strand', 'AD', 'AD.1', 'AF',
           'Consequence', 'IMPACT', 'SYMBOL', 'HGVSc', 'HGVSp', 'CLIN_SIG',
           'PolyPhen', 'SIFT', 'SampleID', 'POLYPHEN', 'POLYSCORE', 'SIFTS',
           'SIFTSCORE'],
          dtype='object')




```python
#select only position and sample ids from whole table 
colon_sample_table = colon_mutation[["SYMBOL","seqnames","start","end", "SampleID"]]
colon_sample_table
```

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
df = master_selected.merge(colon_sample_table, on=cols, how='left')

df = (df.join(pd.get_dummies(df.pop('SampleID')))
        .groupby(cols).max()
        .reindex(colon_sample_table['SampleID'].unique(), axis=1, fill_value=0)
        .reset_index())
```


```python
#View the deleterious matrix
df
```

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
      <td>ABCA4</td>
      <td>1</td>
      <td>94517254</td>
      <td>94517254</td>
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
      <td>ABCA4</td>
      <td>1</td>
      <td>94578618</td>
      <td>94578618</td>
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
      <td>ABCC6</td>
      <td>16</td>
      <td>16248755</td>
      <td>16248755</td>
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
      <td>ABCC6</td>
      <td>16</td>
      <td>16253412</td>
      <td>16253412</td>
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
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ABCC6</td>
      <td>16</td>
      <td>16263524</td>
      <td>16263524</td>
      <td>1</td>
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
      <th>150</th>
      <td>TYR</td>
      <td>11</td>
      <td>88961101</td>
      <td>88961101</td>
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
      <th>151</th>
      <td>TYR</td>
      <td>11</td>
      <td>89017961</td>
      <td>89017961</td>
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
      <th>152</th>
      <td>VHL</td>
      <td>3</td>
      <td>10191605</td>
      <td>10191605</td>
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
      <th>153</th>
      <td>VPS35</td>
      <td>16</td>
      <td>46696364</td>
      <td>46696364</td>
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
      <th>154</th>
      <td>XRCC1</td>
      <td>19</td>
      <td>44051036</td>
      <td>44051036</td>
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
<p>155 rows × 205 columns</p>
</div>




```python
#Save the matrix to local
df.to_csv('master_deleterious_matrix.txt', sep='\t', index=False)
```


```python

```
