
# open_source_sii_data

此仓库包含为 `Harness_Engineering_Exam/student_package` 工作流重新打包和转换后的数据文件。

## 此仓库包含什么

* `data_ood/`

  * 源自 CLINC150 风格的意图分类数据。
  * 已移除范围外（`oos`）样本。
  * 此版本保留较大的派生划分。
* `data_ood_minimal/`

  * `data_ood/` 的较小子集。 
  * 构建目的在于在减少规模的同时，严格保持训练/测试标签集一致。
* `poply/`

  * 在原始任务划分之外发现的额外领域内银行风格意图数据。
  * 根据标签模式和话语风格判断，这些数据似乎源自 BANKING77 或与其密切相关的数据源。
  * 此归因是基于已发布数据结构作出的推断，并非来自原始考试包的已验证声明。
  * 
* `mmlu_ood_choice_in_question/`

  * 源自 MMLU 的多项选择数据。
  * `text` 字段包含问题以及所有 `A. / B. / C. / D.` 形式的选项。
  * `label` 字段仅包含答案字母，例如 `A`、`B`、`C` 或 `D`。
* `mmlu_ood_choice_out_of_question/`

  * 源自 MMLU 的多项选择数据。
  * `text` 字段包含问题以及所有 `A. / B. / C. / D.` 形式的选项。
  * `label` 字段包含完整答案选项，例如 `B. Business ethics management`。
* `mmlu_all_inquestion/`

  * 源自 MMLU 的多项选择数据。
  * `text` 字段包含问题以及所有 `A. / B. / C. / D.` 形式的选项。
  * `label` 字段仅包含答案内容，不包含答案字母。
* `run_1.py`、`run_2.py`、`run_3.py`、`run_4.py`、`run_5.py`

  * 与 student package 代码库配合使用的示例运行脚本。

## 多项选择变体

此仓库包含同一批 MMLU 风格多项选择数据的三个转换变体：

1. `mmlu_ood_choice_in_question`

   * `text`：问题 + `A. / B. / C. / D.` 选项
   * `label`：仅答案字母
2. `mmlu_ood_choice_out_of_question`

   * `text`：问题 + `A. / B. / C. / D.` 选项
   * `label`：答案字母加答案内容
3. `mmlu_all_inquestion`

   * `text`：问题 + `A. / B. / C. / D.` 选项
   * `label`：仅答案内容

## 预期用法

预期用法是将此仓库放在 `student_package` 下，并直接使用其中包含的数据文件夹。

示例布局：

```text
Harness_Engineering_Exam/
  student_package/
      data_ood/
      data_ood_minimal/
      poply/
      mmlu_ood_choice_in_question/
      mmlu_ood_choice_out_of_question/
      mmlu_all_inquestion/
      run_1.py
      ...
```

如果你的代码期望这些文件夹直接位于 `student_package` 下，请避免留下额外嵌套的 Git 仓库层。

示例：

```bash
cd /path/to/Harness_Engineering_Exam/student_package
git clone https://github.com/hustnobody3/open_source_sii_data.git

# If you want the files flattened into the current student_package directory:
rm -rf open_source_sii_data/.git
rsync -av open_source_sii_data/ ./
rm -rf open_source_sii_data
```

完成后，你的 `student_package` 可以直接包含：

```text
student_package/
  data_ood/
  data_ood_minimal/
  poply/
  mmlu_ood_choice_in_question/
  mmlu_ood_choice_out_of_question/
  mmlu_all_inquestion/
  run_1.py
  ...
```

## 免责声明

* 此仓库只是对现有公开数据集以及在已发布考试包上下文中发现的文件进行重新打包和转换。
* 此仓库的维护者不是 CLINC150、MMLU、BANKING77 或考试材料的原始作者、许可方或官方分发者。
* 维护者不声称拥有原始数据集的所有权。
* 对于使用此仓库所获得的基准测试分数、实验结论、下游失败、标注问题、格式问题或任何其他结果，维护者不承担责任。
* 维护者不对使用者任何成绩负责，维护者不是最终数据的参与维护者，数据来源完全来自个人猜测和自我使用以及开源，如果内含最终测试数据，维护者不对此负任何责任，纯属偶然
* 该数据集不一定为最后测试数据，若有结果偏置，不对最后的结果做任何保证，因此，谨慎相信和使用该数据
* **请不要开盒作者**
* 如果你发现数据质量问题、格式问题、不正确的来源声明或其他问题，请提交 issue 或 PR。

## 来源说明

* `data_ood/` 和 `data_ood_minimal/` 源自 CLINC150 风格的数据，其中移除了范围外样本，并构建了新的训练/测试子集。
* `mmlu_*` 目录源自标准的 57 个 MMLU 学科目录，并转换为文本分类风格的 JSONL 文件。
* `poply/` 包含额外的领域内银行风格意图数据，这些数据未包含在本地工作流所使用的原始源任务划分中。
* 关于领域内银行数据与 BANKING77 相关的说法，是基于标签和样本结构作出的有根据推断。

## 文件格式

所有数据集均以 JSONL 格式存储。

每一行都是一个单独的 JSON 对象：

```json
{"text": "example input", "label": "example label"}
```

## 上游数据集的建议引用

如果你在论文、报告或公开基准测试中使用这些转换后的文件，请引用原始上游数据集或基准论文，而不是仅引用此仓库。

### MMLU

```bibtex
@article{hendrycks2020mmlu,
  title={Measuring Massive Multitask Language Understanding},
  author={Hendrycks, Dan and Burns, Collin and Basart, Steven and Zou, Andy and Mazeika, Mantas and Song, Dawn and Steinhardt, Jacob},
  journal={arXiv preprint arXiv:2009.03300},
  year={2020},
  url={https://arxiv.org/abs/2009.03300}
}
```

### CLINC150

```bibtex
@inproceedings{larson2019clinc150,
  title={An Evaluation Dataset for Intent Classification and Out-of-Scope Prediction},
  author={Larson, Stefan and Mahendran, Anish and Peper, Joseph J. and Clarke, Christopher and Lee, Andrew and Hill, Parker and Kummerfeld, Jonathan K. and Leach, Kevin and Laurenzano, Michael A. and Tang, Lingjia and Mars, Jason},
  booktitle={Proceedings of the 2019 Conference on Empirical Methods in Natural Language Processing and the 9th International Joint Conference on Natural Language Processing (EMNLP-IJCNLP)},
  pages={1311--1316},
  year={2019},
  url={https://aclanthology.org/D19-1131/},
  doi={10.18653/v1/D19-1131}
}
```

### BANKING77

```bibtex
@inproceedings{casanueva2020banking77,
  title={Efficient Intent Detection with Dual Sentence Encoders},
  author={Casanueva, I{\~n}igo and Temcinas, Tadas and Gerz, Daniela and Henderson, Matthew and Vulic, Ivan},
  booktitle={Proceedings of the 2nd Workshop on NLP for Conversational AI},
  year={2020},
  note={Data available at https://github.com/PolyAI-LDN/task-specific-datasets},
  url={https://arxiv.org/abs/2003.04807}
}
```

## 备注


* 欢迎提交 PR 来改进来源说明、数据验证、格式一致性和文档。
