## Adversarial evaluation of model performances [Updated]

Here is an example of evaluating a model (fine-tuned either on MNLI or SNLI) using adversarial evaluation of natural language inference with the Heuristic Analysis for NLI Systems (HANS) dataset [McCoy et al., 2019](https://arxiv.org/abs/1902.01007).

The HANS dataset can be downloaded from [this location](https://github.com/tommccoy1/hans).

This is an example of using run_hans_mnli.py in Google Colab:

```bash
!git clone https://github.com/mhdr3a/transformers-hans
!mv /content/transformers-hans/* /content/
!rm transformers-hans -r
!pip install -r requirements.txt

!git clone https://github.com/tommccoy1/hans
!mv /content/hans/* /content/
!rm hans -r

!python run_hans_mnli.py \
        --task_name hans \
        --do_eval \
        --data_dir ./ \
        --model_name_or_path mnli-6 \
        --max_seq_length 128 \
        --output_dir mnli-6
```
* Note that the mnli-6 model is fine-tuned on MNLI; use run_hans_snli.py if your model is fine-tuned on SNLI.

This will create the hans_predictions.txt file in ./mnli-6, which can then be evaluated using evaluate_heur_output.py from the HANS dataset.

```bash
!python evaluate_heur_output.py ./mnli-6/hans_predictions.txt
```

The evaluation results for the [mnli-6 model](https://huggingface.co/mahdiyar/mnli-6) is as follows:

```bash
Heuristic entailed results:
lexical_overlap: 0.9932
subsequence: 1.0
constituent: 0.9882

Heuristic non-entailed results:
lexical_overlap: 0.6494
subsequence: 0.2434
constituent: 0.353

Subcase results:
ln_subject/object_swap: 0.973
ln_preposition: 0.847
ln_relative_clause: 0.774
ln_passive: 0.134
ln_conjunction: 0.519
le_relative_clause: 0.979
le_around_prepositional_phrase: 1.0
le_around_relative_clause: 1.0
le_conjunction: 0.987
le_passive: 1.0
sn_NP/S: 0.0
sn_PP_on_subject: 0.56
sn_relative_clause_on_subject: 0.491
sn_past_participle: 0.038
sn_NP/Z: 0.128
se_conjunction: 1.0
se_adjective: 1.0
se_understood_object: 1.0
se_relative_clause_on_obj: 1.0
se_PP_on_obj: 1.0
cn_embedded_under_if: 0.692
cn_after_if_clause: 0.0
cn_embedded_under_verb: 0.567
cn_disjunction: 0.0
cn_adverb: 0.506
ce_embedded_under_since: 0.942
ce_after_since_clause: 1.0
ce_embedded_under_verb: 0.999
ce_conjunction: 1.0
ce_adverb: 1.0

Template results:
temp1: 0.973
temp5: 0.910828025477707
temp7: 0.9639175257731959
temp3: 0.8786127167630058
temp2: 0.632768361581921
temp4: 0.9736842105263158
temp6: 0.7142857142857143
temp11: 0.8452380952380952
temp9: 0.7227722772277227
temp15: 0.49
temp16: 0.9875
temp10: 0.9634146341463414
temp8: 0.2463768115942029
temp18: 0.782608695652174
temp12: 0.9012345679012346
temp14: 0.7530864197530864
temp19: 0.9069767441860465
temp13: 0.8421052631578947
temp17: 0.8529411764705882
temp21: 0.12525252525252525
temp20: 0.14257425742574256
temp22: 0.1694915254237288
temp25: 0.5394736842105263
temp24: 0.865979381443299
temp23: 0.42448979591836733
temp28: 0.96875
temp26: 0.9924812030075187
temp29: 0.9683794466403162
temp27: 0.9866666666666667
temp30: 1.0
temp31: 1.0
temp32: 0.991869918699187
temp33: 0.9822834645669292
temp36: 1.0
temp35: 1.0
temp37: 0.0
temp38: 0.56
temp39: 0.491
temp40: 0.0
temp41: 0.09382716049382717
temp42: 0.10235294117647059
temp43: 0.2733333333333333
temp44: 1.0
temp45: 1.0
temp46: 1.0
temp47: 1.0
temp48: 1.0
temp49: 1.0
temp50: 0.692
temp51: 0.0
temp52: 0.567
temp53: 0.0
temp54: 0.0
temp58: 0.506
temp59: 0.942
temp60: 1.0
temp61: 0.999
temp63: 1.0
temp62: 1.0
temp68: 1.0
```

And here are the evaluation results for the [snli-6 model](https://huggingface.co/mahdiyar/snli-6):

```bash
Heuristic entailed results:
lexical_overlap: 0.9778
subsequence: 0.9696
constituent: 0.9658

Heuristic non-entailed results:
lexical_overlap: 0.6202
subsequence: 0.1618
constituent: 0.1974

Subcase results:
ln_subject/object_swap: 0.929
ln_preposition: 0.796
ln_relative_clause: 0.717
ln_passive: 0.038
ln_conjunction: 0.621
le_relative_clause: 0.981
le_around_prepositional_phrase: 1.0
le_around_relative_clause: 0.993
le_conjunction: 0.924
le_passive: 0.991
sn_NP/S: 0.001
sn_PP_on_subject: 0.411
sn_relative_clause_on_subject: 0.227
sn_past_participle: 0.042
sn_NP/Z: 0.128
se_conjunction: 0.98
se_adjective: 0.999
se_understood_object: 0.869
se_relative_clause_on_obj: 1.0
se_PP_on_obj: 1.0
cn_embedded_under_if: 0.573
cn_after_if_clause: 0.023
cn_embedded_under_verb: 0.156
cn_disjunction: 0.039
cn_adverb: 0.196
ce_embedded_under_since: 0.873
ce_after_since_clause: 0.984
ce_embedded_under_verb: 0.99
ce_conjunction: 0.982
ce_adverb: 1.0

Template results:
temp1: 0.929
temp5: 0.910828025477707
temp7: 0.9329896907216495
temp3: 0.7976878612716763
temp2: 0.7062146892655368
temp4: 0.7763157894736842
temp6: 0.6190476190476191
temp11: 0.75
temp9: 0.6831683168316832
temp15: 0.42
temp16: 0.975
temp10: 0.7682926829268293
temp8: 0.43478260869565216
temp18: 0.8913043478260869
temp12: 0.7654320987654321
temp14: 0.7037037037037037
temp19: 0.7674418604651163
temp13: 0.5921052631578947
temp17: 0.8823529411764706
temp21: 0.03838383838383838
temp20: 0.03762376237623762
temp22: 0.2796610169491525
temp25: 0.8421052631578947
temp24: 0.7972508591065293
temp23: 0.5346938775510204
temp28: 0.9921875
temp26: 0.9774436090225563
temp29: 0.9565217391304348
temp27: 1.0
temp30: 1.0
temp31: 0.993
temp32: 1.0
temp33: 0.8503937007874016
temp36: 0.9918367346938776
temp35: 0.9901960784313726
temp37: 0.001
temp38: 0.411
temp39: 0.227
temp40: 0.020168067226890758
temp41: 0.07407407407407407
temp42: 0.09411764705882353
temp43: 0.32
temp44: 0.9675850891410048
temp45: 1.0
temp46: 0.999
temp47: 0.869
temp48: 1.0
temp49: 1.0
temp50: 0.573
temp51: 0.023
temp52: 0.156
temp53: 0.044585987261146494
temp54: 0.034026465028355386
temp58: 0.196
temp59: 0.873
temp60: 0.984
temp61: 0.99
temp63: 0.9942307692307693
temp62: 0.96875
temp68: 1.0
```
