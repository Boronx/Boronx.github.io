---
layout: post
icon: fas fa-quote-left
order: 2
---

<script>
function copyText(textToCopy) {
    const text = document.getElementById(textToCopy).innerText;
    console.log(text);  // Check what text is grabbed
    navigator.clipboard.writeText(text).then(() => {
        alert('BibTeX copied to clipboard!');
    }).catch(err => {
        console.error('Failed to copy text: ', err);
    });
}
</script>

# yes

## **Publications**

### [Chat2Scenario: Scenario Extraction From Dataset Through Utilization of Large Language Model](https://graz.elsevierpure.com/en/publications/chat2scenario-scenario-extraction-from-dataset-through-utilizatio)

_Yongqi Zhao, **Wenbo Xiao\***, Tomislav Mihalj, Jia Hu and Arno Eichberger<br>_
_In Arxiv (Preprint), IEEE IV Accepted, 2024_

<a href="https://arxiv.org/pdf/2404.16147" class="tag"><small>PDF</small></a>
<a href="https://github.com/ftgTUGraz/Chat2Scenario" class="tag"><small>CODE</small></a>
<a href="#" onclick="copyText('Cite_chat2s'); return false;" class="tag"><small>BibTeX</small></a>

<p id="Cite_chat2s" class="hidden-text">
@misc{zhao2024chat2scenario,
      title={Chat2Scenario: Scenario Extraction From Dataset Through Utilization of Large Language Model}, 
      author={Yongqi Zhao and Wenbo Xiao and Tomislav Mihalj and Jia Hu and Arno Eichberger},
      year={2024},
      eprint={2404.16147},
      archivePrefix={arXiv},
      primaryClass={cs.RO}
}
</p>

### [Research on the Occupant Discomfort due to Safety Perception in Overtaking Scenarios](https://www.sae.org/publications/technical-papers/content/2022-01-7089/)

_Xingyu Zhao, **Wenbo Xiao**, Tao Zhou, Haolan Meng_<br>
_SAE 2022 Intelligent and Connected Vehicles Symposium, ICVS 2022, Shanghai_

<a href="/assets/papers/Research_on_the_Occupant_Discomfort_Due_to_Safety_Perception_in_Overtaking_Scenarios.pdf" class="tag"><small>PDF</small></a>
<a href="#" onclick="copyText('Cite_discomfortZhao'); return false;" class="tag"><small>BibTeX</small></a>

<p id="Cite_discomfortZhao" class="hidden-text">
@inproceedings{2022-01-7089,
  author={Xingyu, Zhao and Xiao, Wenbo and Zhou, Tao and Meng, Haolan},
  title={Research on the Occupant Discomfort due to Safety Perception in Overtaking Scenarios},
  booktitle={SAE 2022 Intelligent and Connected Vehicles Symposium},
  publisher={SAE International},
  month={dec},
  year={2022},
  doi={https://doi.org/10.4271/2022-01-7089},
  url={https://doi.org/10.4271/2022-01-7089},
  issn={0148-7191},
  abstract={With the widespread application of autonomous driving technology, occupant comfort has become a key topic. Occupant comfort of autonomous vehicles depends on the driving system’s performance, so studying the causes of occupant discomfort will help design driving systems. In addition to the discomfort in NVH and thermal comfort, occupant comfort is also affected by other factors such as safety perception. To study the impact of safety perception on comfort, this paper designed a road experiment and focused on the overtaking scenarios. Because the interaction between the ego vehicle and others is strong during overtaking, the occupants are more likely to receive visual stimuli, resulting in discomfort caused by safety perception. In the experiment, occupant discomfort scores were collected in real-time by the tool developed in this paper. Meanwhile, the kinematics data and video were collected and used to calculate eight indexes related to safety perception: the ego vehicle speed, the relative speed with the front vehicle, TTC, the position of adjacent background vehicles, longitudinal distance from the front vehicle, the model of the vehicle in front, the ego vehicle acceleration, and the overtaking time. After correlation analysis, it can be found that at a significant level of 0.05, the first four indexes are closely related to the discomfort score. Then, the first four indexes were used as independent variables, and the discomfort score was used as a dependent variable to be substituted into the multiple linear regression model to analyze different effects on comfort. The results show that choosing to overtake when a vehicle is in the target lane will increase the discomfort by 28.1%, compared with the scenario where no vehicle is around the vehicle. In addition, if the vehicle’s speed increases by 1m/s or the TTC decreases by 1s, the occupant discomfort will increase by 0.02 and 0.018.}
}
</p>

## **Patent**

- Classification and Coding Methods of Driving Scenarios  
  _`Chinese patent`_ _`Number: CN202210473739.9`_
- Classification and Coding Methods of Driving Scenarios  
  `Chinese patent` `Number: CN202210473739.9`

---

## **Projects**

### [PECOP - Key Technology of PErception and Control in COoperative Vehicle-Infrastructure System for Urban Public Transportation](https://graz.elsevierpure.com/en/projects/pecop-key-technology-of-perception-and-control-in-cooperative-veh) `TUG` `TJU`

> _International coopperative R&D project between China and Austria_

- **Website:**
- **My role:** XXX

### [Toolchain for Simulation and Digital-twin-based Evaluation of ADS](https://it.chd.edu.cn/2022/0130/c7383a210861/page.htm) `TJU`

> _National Key Research and Development Program (2021YFB2501200)_ <br> _In Chinese: 国家重点研发计划项目“自动驾驶仿真及数字孪生测试评价工具链”_

- **Website:** [_http://www.cavtetc.cn/_](http://www.cavtetc.cn/)
- **My role:** XXX

### Scenario classification `TJU`

### Perceived Safety for Vehicel Occupants `TJU`

>
