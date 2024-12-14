---
tags:
- ASL
url: https://signllm.github.io/
---

## **SignLLM: Sign Languages Production Large Language Models

<table id="u-table"><tbody><tr><td><center><span><sup>1</sup>Rutgers University</span></center></td><td><center><span><sup>2</sup>Australian National University</span></center></td><td><center><span><sup>3</sup>Data61/CSIRO</span></center></td><td><center><span><sup>4</sup>Carnegie Mellon University</span></center></td></tr></tbody></table>

<table id="u-table"><tbody><tr><td><center><span><sup>5</sup>Columbia University</span></center></td><td><center><span><sup>6</sup>University of Texas at Dallas</span></center></td><td><center><span><sup>7</sup>University of Central Florida</span></center></td></tr></tbody></table>

___

<table><tbody><tr><td><center><a href="https://signllm.github.io/resources/images/cover_v12.drawio.png"><img src="https://signllm.github.io/resources/images/cover_v12.drawio.png" width="800px"></a><br></center></td></tr><tr><td><center><span><i><b>Overview:</b> (Left) Major components(e.g., Text, Prompt, Compressed Pose, etc.) of Prompt2Sign dataset. Compressed Pose is reprocessed pose data that is suitable for training, we use public sign language videos to produce compressed pose data in our predefined format; (Right) Our proposed SignLLM aims to generate sign language poses for various application scenarios.</i></span></center></td></tr></tbody></table>

<table id="u-table"><tbody><tr><td><center><a href="https://arxiv.org/abs/2405.10718v1"><img onmouseover="this.src='./resources/images/paper.png';" onmouseout="this.src='./resources/images/paper.png';" src="https://signllm.github.io/resources/images/paper.png" height="120px"></a><br><span>Paper</span><br></center></td><td><center><a href="https://signllm.github.io/Prompt2Sign"><img onmouseover="this.src='./resources/images/data_icon.png';" onmouseout="this.src='./resources/images/data_icon.png';" src="https://signllm.github.io/resources/images/data_icon.png" height="120px"></a><br><span>Prompt2Sign (tools)</span><br></center></td><td><center><a href="https://signllm.github.io/#demo"><img onmouseover="this.src='./resources/images/video_icon.png';" onmouseout="this.src='./resources/images/video_icon.png';" src="https://signllm.github.io/resources/images/video_icon.png" height="120px"></a><br><span>Additional details</span><br></center></td><td><center><a href="https://signllm.github.io/#analysis"><img onmouseover="this.src='./resources/images/magnify_glass.png';" onmouseout="this.src='./resources/images/magnify_glass.png';" src="https://signllm.github.io/resources/images/magnify_glass.png" height="120px"></a><br><span>Methodology</span><br></center></td><td><center><a href="https://github.com/SignLLM/"><img onmouseover="this.src='./resources/images/github_icon.png';" onmouseout="this.src='./resources/images/github_icon.png';" src="https://signllm.github.io/resources/images/github_icon.png" height="120px"></a><br><span>Code (stay tuned)</span><br></center></td></tr></tbody></table>

Subscribe to the latest news of SignLLM by [Google Forms](https://forms.gle/Sdw3NAM7Q5Ybxi7YA).

___

## Abstract

  In this paper, we propose SignLLM, a multilingual Sign Language Production (SLP) large language model, which includes two novel multilingual SLP modes MLSF and Prompt2LangGloss that allow sign language gestures generation from query texts input and question-style prompts input respectively. Both modes can use a new RL loss based on reinforcement learning and a new RL module named Priority Learning Channel. These RL components can accelerate the training by enhancing the model's capability to sample high-quality data. For SignLLM's training, we introduce Prompt2Sign, a comprehensive multilingual sign language dataset, which builds from public data, including American Sign Language (ASL) and seven others. This dataset standardizes information by extracting pose information from sign language videos into a unified compressed format. We extensively evaluate SignLLM, demonstrating that our model achieves state-of-the-art performance on SLP tasks across eight sign languages.

Besides the abstract, you can also read the unofficial [English](https://www.marktechpost.com/2024/05/30/signllm-a-multilingual-sign-language-model-that-can-generate-sign-language-gestures-from-input-text/) or [Chinese](https://mp.weixin.qq.com/s/qrUGYDN9URIxQ8kmhdaCmw) paper interpretation.

___

## Demo Video

<table><tbody><tr><td><video width="200" height="200" controls="" autoplay="" loop="" muted="" playsinline="" src="https://signllm.github.io/resources/videos/p1.mp4" frameborder="0"></video></td><td><video width="200" height="200" controls="" autoplay="" loop="" muted="" playsinline="" src="https://signllm.github.io/resources/videos/p2.mp4" frameborder="0"></video></td><td><video width="200" height="200" controls="" autoplay="" loop="" muted="" playsinline="" src="https://signllm.github.io/resources/videos/p4.mp4" frameborder="0"></video></td></tr><tr><td></td><td></td><td></td></tr><tr><td colspan="3"><span><i>DEMO: We give some examples of better prediction results, below each video is their input text.</i></span></td></tr></tbody></table>

___

## Qualitative Presentation (Multilingual)

<table><tbody><tr><td><video width="200" height="282" controls="" autoplay="" loop="" muted="" playsinline="" src="https://signllm.github.io/resources/videos8/asl_vid3.mp4" frameborder="0"></video></td><td><video width="200" height="282" controls="" autoplay="" loop="" muted="" playsinline="" src="https://signllm.github.io/resources/videos8/gsl_vid3.mp4" frameborder="0"></video></td><td><video width="200" height="282" controls="" autoplay="" loop="" muted="" playsinline="" src="https://signllm.github.io/resources/videos8/ksl_vid2.mp4" frameborder="0"></video></td><td><video width="200" height="282" controls="" autoplay="" loop="" muted="" playsinline="" src="https://signllm.github.io/resources/videos8/dsgs_vid3.mp4" frameborder="0"></video></td></tr><tr><td><p><strong>ASL</strong></p><div><p><span><i>Input: Here's a little example here I'm going to give you some insight on though.</i><br><i>Translation: Here's a little example here I'm going to give you some insight on though.</i></span></p></div></td><td><p><strong>DGS</strong></p><div><p><span><i>Input: Im Südostraum ist es vorteilhaft, ein Hochdruckgebiet kommt von Belgien.</i><br><i>Translation: In the southeastern region it is advantageous, a high-pressure system is coming from Belgium.</i></span></p></div></td><td><p><strong>KSL</strong></p><div><p><span><i>Input: 염려하다.</i><br><i>Translation: worried about.</i></span></p></div></td><td><p><strong>DSGS</strong></p><div><p><span><i>Input: Bei dieser Firma bestelle ich immer die Plastikbecher.</i><br><i>Translation: I always order plastic cups from this company.</i></span></p></div></td></tr><tr><td><video width="200" height="282" controls="" autoplay="" loop="" muted="" playsinline="" src="https://signllm.github.io/resources/videos8/lsf_vid2.mp4" frameborder="0"></video></td><td><video width="200" height="282" controls="" autoplay="" loop="" muted="" playsinline="" src="https://signllm.github.io/resources/videos8/lis_vid3.mp4" frameborder="0"></video></td><td><video width="200" height="282" controls="" autoplay="" loop="" muted="" playsinline="" src="https://signllm.github.io/resources/videos8/lsa_vid4.mp4" frameborder="0"></video></td><td><video width="200" height="282" controls="" autoplay="" loop="" muted="" playsinline="" src="https://signllm.github.io/resources/videos8/tsl_vid2.mp4" frameborder="0"></video></td></tr><tr><td><p><strong>LSF-CH</strong></p><div><p><span><i>Input: Le leader du parti socialiste.</i><br><i>Translation: The leader of the Socialist Party.</i></span></p></div></td><td><p><strong>LIS-CH</strong></p><div><p><span><i>Input: Io voglio comprare una nuova borsa.</i><br><i>Translation: I want to buy a new bag.</i></span></p></div></td><td><p><strong>LSA</strong></p><div><p><span><i>Input: desayuno.</i><br><i>Translation: breakfast.</i></span></p></div></td><td><p><strong>TSL</strong></p><div><p><span><i>Input: Animasyon atölyesinde 9-12 yaş arası işitme engelli çocuklar animasyon sanatını öğrenecekler.</i><br><i>Translation: Children who are deaf or hard of hearing (aged 9-12) will learn about animation art at the animation workshop.</i></span></p></div></td></tr><tr><td colspan="4"><span><i>QP: Synthetic sign language video generated through style transfer modeling (intermediate input video has undergone processing like acceleration and rendering; results under Ideal Future Conditions).</i></span></td></tr></tbody></table>

___

## Main Method

<table><tbody><tr><td><center><a><img src="https://signllm.github.io/resources/images/method_v2.drawio.png" width="800px"></a><br></center></td></tr><tr><td><center><span><i>(Left) MLSF contains parallel Enc-Dec groups (i.e., Text2Pose × number of languages), the Prompt2LangGloss adds a language attribute marker at the gloss channel (i.e., Text2Gloss2Pose → Prompt2LangGloss2Pose). (Right) The output of SignLLM can be converted into a skeletal pose video, which can then be rendered into a realistic human appearance by vid2vid models.</i></span></center></td></tr></tbody></table>

___

## Other Method

In our work, we have improved upon the Text2Gloss framework by incorporating a marker that produces Gloss with the necessary linguistic attributes, while also representing profound characteristics through variables V<sub>t</sub> and X<sub>u</sub> within neural networks. Additionally, we have introduced five key elements—user, agent, environment, iterative update process, and PLC—which collectively outline a reinforcement learning process tailored for sequence prediction.

![Reinforcement Learning Process](https://signllm.github.io/resources/images/RL.drawio_v2.png) ![Text to Language Gloss Framework](https://signllm.github.io/resources/images/text2langgloss_v2.drawio.png)

___

## Empirical Studies and Analysis

## (1) American Sign Language Production (ASLP).

<table><tbody><tr><td><center><a><img src="https://signllm.github.io/resources/images/1.png"></a><br></center></td></tr><tr><td><span><i>Comparison of different models of SignLLM with baseline. Models M and T represent MLSF and Text2LangGloss trained ASLP models, respectively.</i></span></td></tr></tbody></table>

## (2) German Sign Language Production (GSLP).

<table><tbody><tr><td><center><a><img src="https://signllm.github.io/resources/images/2.png"></a><br></center></td></tr><tr><td><span><i>Comparison of different models of SignLLM with previous work.</i></span></td></tr></tbody></table>

## (3) Ablation Study.

<table><tbody><tr><td><center><a><img src="https://signllm.github.io/resources/images/3.png"></a><br></center></td></tr><tr><td><span><i>SignLLM-40M-Base results for Text to Pose on the ASL part of Prompt2Sign, with multiple data augmentation techniques. Base: Multi-Language Switching Framework with Normal MSE Loss, FP: Future Prediction, GN: Gaussian Noise, Text2LangGloss: Text2LangGloss with Normal MSE Loss, PLC: Priority Learning Channe</i></span></td></tr></tbody></table>

## (4) Training Efficiency Study.

<table><tbody><tr><td><center><a><img src="https://signllm.github.io/resources/images/4.png"></a></center></td></tr><tr><td><span><i>the comparison of the effect of different Settings on DTW values (the lower the better) at different times is determined by epoch.</i></span></td></tr></tbody></table>

___

## Updates

\[2024.06.30\] The [Jupyer Notebook](https://github.com/SignLLM/Prompt2Sign/blob/main/tools/2D_to_3D/run.ipynb) and [Docker](https://www.codewithgpu.com/i/SignLLM/Prompt2Sign/Prompt2Sign) for data processing has been released.

\[2024.05.17\] The [arXiv version](https://arxiv.org/abs/2405.10718) of the paper is now available.

\[2024.01.16\] Prompt2Sign homepage is available and data is expected to be released after accept (maybe at the end of 2024, so don't rush).

\[2023.12.14\] We have made supplementary materials and demo available at this page.

\[2023.11.04\] We have made Prompt2Sign and Tools available at GitHub. Check out [here](https://github.com/SignLLM/Prompt2Sign).

## FAQs

Q0: License issue:

A0: The Prompt2Sign and SignLLM are copyright by us and published under the Creative Commons Attribution-NonCommercial 4.0 International License. Some subsets need to be implemented by users themselves.

Q1: Some links are invalid on page. How can I obtain the missing information?

Q1: I am located in mainland China and I cannot access Google Driver. How can I get the dataset?

A1: Please submit a GitHub issue at [Any repository of user "SignLLM"](https://github.com/SignLLM). We may reach you shortly.

Q2: Is the data in the data set complete relative to the original video? I feel like it's smaller than the actual data set.

A2: We're using a dataset that is a subset of the video clips that correspond to the lines and then we compress those clips. Compression to 1/5 of the original size refers to 1/5 of the size of the clip.

Q3: Can we fully achieve the actual effect in the paper or presentation?

A3: No, according to the data and the actual situation, most of our cases are not up to the level of use. Dynamic or static display, we are selected to show the best effect. Q4: How to complete the data conversion format? Specific to the level of each number. Too much remains unclear.

A4: You can look at the [dataset](https://signllm.github.io/Prompt2Sign/) itself and the [tools](https://github.com/SignLLM/Prompt2Sign), with an example and plenty of text describing it in detail.

## How to finish data format conversion (JSON->Ours)?

Below, we show an example JSON:

```
### JSON file:
{
    "version": 1.3,
    "people": [
        {
            "person_id": [
                -1
            ],
            "pose_keypoints_2d": [
                666.535,
                219.883,
                ...
        # We only get eight key points in the upper body(24 number).
            ],
            "face_keypoints_2d": [
                624.108,
                204.299,
                0.813047,
                # We don't train the face.
            ],
            "hand_left_keypoints_2d": [
                694.829,
                455.679,
                0.352355,
                ...
# 21 key points, 63 values.

            ],
            "hand_right_keypoints_2d": [
                516.344,
                348.757,
                0.0184774,
                ...
// 21 key points, 63 values.
            ],
            "pose_keypoints_3d": [],
            "face_keypoints_3d": [],
            "hand_left_keypoints_3d": [],
            "hand_right_keypoints_3d": []
        }
    ]
}

```

**How to extract key points?** We extracted two-dimensional (2D) frontal human pose information from videos of different resolutions, including upper body pose information of the body and hands, through [OpenPose](https://github.com/CMU-Perceptual-Computing-Lab/openpose). Includes 8 upper body key points. 21 keypoints in each hand, which is a total of 42 hand keypoints. These two parts add up to fifty keypoints, each of which has three XYZ messages, or 150 numbers.

Then in steps \`\`json (2D keypoints) to h5'', \`\`h5 to txt (3D keypoints)'', and \`\`txt to skels (Standard Pose Storage)'':

**How to complete \`\`json to h5''?** We successively obtain a json number in a folder (a frame of pose information, 50 key points, 150 numbers), and then read all the json numbers in a folder into the key name of an h5 (h5 is a format of numpy) file, multiple folders form multiple build names, and finally form an h5 file.

**How to complete \`\`h5 to txt''?** We read each key name of h5 in turn (the original folder name), create the corresponding folder, each folder generates 5 txt files, the last one is the result, the first 4 txt stores the intermediate variable. This is the part of 2D to 3D, and the key formula 3 in the text is the formula of this part. Additionally, we read the relevant data and delete the unqualified data such as NaN, 0, or replace it with the average median of the data. Finally, we condensed the data to about 1/5 of the original, this data comes from the processing of ASL part.

**How to complete \`\`txt to skels''?** We read the fifth txt file of each folder in turn, the number of lines in the txt file represents the number of frames of the folder corresponding to the video, we read a line of txt (150 numbers, separated by Spaces, a frame of information), plus a space, and then add a count value (the current line divided by the total number of lines, representing the progress bar), add a space after the count value, Then add the second line txt and continue to repeat the above. Then we put a txt (a video information, the total number of numbers in it = 151\* video frames) into a line of content, in turn, tens of thousands of videos are all stored in our standard format.

## How to complete h5 to txt conversion?

Above you mentioned TXT folder 12345, but what is TXT5? Below, we show an example the above data processing process:

```
def getTXT(key, fnameIn, i, mode):
  output_file = f"out_data/{mode}/{key}/demo5.txt"
  if os.path.exists(output_file):
            print(f"Skipping {key} as output file already exists.")
            return
  else:
      # Getting our structure of skeletal model.
      # For customizing the structure see a definition of getSkeletalModelStructure. 
      dtype = "float32"
      randomNubersGenerator = numpy.random.RandomState(1234) 
      structure = skeletalModel.getSkeletalModelStructure()
      with h5py.File(fnameIn, "r") as hfIn:
            print("")
            print("Now is processing the "+ key)
            print("")
            inputSequence_2D = numpy.array(hfIn.get(key))

            # Decomposition of the single matrix into three matrices: x, y, w (=likelihood)
            X = inputSequence_2D
            print(X.shape)
            Xx = X[0:X.shape[0], 0:(X.shape[1]):3]
            Xy = X[0:X.shape[0], 1:(X.shape[1]):3]
            Xw = X[0:X.shape[0], 2:(X.shape[1]):3]

            # Normalization of the picture (x and y axis has the same scale)
            Xx, Xy = pose2D.normalization(Xx, Xy)
            save(f"out_data/{mode}/{key}/demo1.txt", [Xx, Xy, Xw])

            # Delete all skeletal models which have a lot of missing parts.
            Xx, Xy, Xw = pose2D.prune(Xx, Xy, Xw, (0, 1, 2, 3, 4, 5, 6, 7), 0.3, dtype)
            save(f"out_data/{mode}/{key}/demo2.txt", [Xx, Xy, Xw])

            # Preliminary filtering: weighted linear interpolation of missing points.
            Xx, Xy, Xw = pose2D.interpolation(Xx, Xy, Xw, 0.99, dtype)
            save(f"out_data/{mode}/{key}/demo3.txt", [Xx, Xy, Xw])

            # Initial 3D pose estimation
            ... = pose2Dto3D.initialization(
                ...
              )
            save(f"out_data/{mode}/{key}/demo4.txt", [Yx0, Yy0, Yz0])

              # Backpropagation-based filtering
            Yx, Yy, Yz = pose3D.backpropagationBasedFiltering(
                ...
              )
            save(f"out_data/{mode}/{key}/demo5.txt", [Yx, Yy, Yz])
            # Called after each folder is processed to release GPU resources
            print(f"Now we're working on folder {i} th, and will be finished")
            i=i+1
            tf.keras.backend.clear_session()

```

The above [code](https://github.com/SignLLM/Prompt2Sign/blob/main/2Dto3D/pipeline_demo_02_h5totxt_train.py) shows the contents of our several TXT files, and it clearly shows that 1234 is mainly to store intermediate variables and related content, the fifth folder is the final product we need. And for more details, see the [official documentation](https://signllm.github.io/Prompt2Sign/).

___

## Paper

___

## Cite

```
@misc{fang2024signllm,
      title={SignLLM: Sign Languages Production Large Language Models}, 
      author={Sen Fang and Lei Wang and Ce Zheng and Yapeng Tian and Chen Chen},
      year={2024},
      eprint={2405.10718},
      archivePrefix={arXiv},
      primaryClass={cs.CV}
}

```

___

## Acknowledgements

We sincerely appreciate the previous work, open source tools, and researchers for underserved populations. We stand on the shoulders of their work to achieve further achievements. Readers can learn how we utilize and improve previous work through our citations.

Additionally, we have noticed spontaneous promotion from over 80-120 marketing media outlets and independent content creators, but they may have some misconceptions or exaggerations about our model. Our model takes input text or prompts to generate videos of sign language pose in various languages. Certain conditions need to be input into the model for further processing to obtain the final videos, so we need to work even harder to strengthen the end-to-end capabilities (ie, the pose video output from the model needs to be processed to achieve the effect of real people).

We are grateful to our supporters including Microsoft, Amazon, Swiss TV, as well as organizations and accessibility practitioners worldwide for their continued support.

___

## Contact

For further questions and suggestions, please only contact [Sen Fang](mailto:sen.fang@rutgers.edu) or [SignLLM](mailto:signllm@googlegroups.com).

[[American Sign Language (ASL)]]