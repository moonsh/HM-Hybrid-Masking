
[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/hmfs-hybrid-masking-for-few-shot-segmentation/few-shot-semantic-segmentation-on-pascal-5i-1)](https://paperswithcode.com/sota/few-shot-semantic-segmentation-on-pascal-5i-1?p=hmfs-hybrid-masking-for-few-shot-segmentation)

[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/hmfs-hybrid-masking-for-few-shot-segmentation/few-shot-semantic-segmentation-on-coco-20i-1)](https://paperswithcode.com/sota/few-shot-semantic-segmentation-on-coco-20i-1?p=hmfs-hybrid-masking-for-few-shot-segmentation)

[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/hmfs-hybrid-masking-for-few-shot-segmentation/few-shot-semantic-segmentation-on-fss-1000-1)](https://paperswithcode.com/sota/few-shot-semantic-segmentation-on-fss-1000-1?p=hmfs-hybrid-masking-for-few-shot-segmentation)

[![PWC](https://img.shields.io/endpoint.svg?url=https://paperswithcode.com/badge/hmfs-hybrid-masking-for-few-shot-segmentation/few-shot-semantic-segmentation-on-coco-20i)](https://paperswithcode.com/sota/few-shot-semantic-segmentation-on-coco-20i?p=hmfs-hybrid-masking-for-few-shot-segmentation)


## HM: Hybrid Masking for Few-Shot Segmentation (ECCV 2022)
The paper is on [[arXiv](https://arxiv.org/abs/2203.12826)].


<p align="middle">
    <img src="figure/main_fig2.png" width="600" height="350" />
</p>


## Scripts
This work can be implemented very easily by using the below script. 
The below script needs to be added to the [HSNet](https://github.com/juhongm999/hsnet), [VAT](https://github.com/Seokju-Cho/Volumetric-Aggregation-Transformer) and [ASNet](https://github.com/dahyun-kang/ifsl).

            supprot_img_im = torch.zeros_like(support_img)            
            supprot_img_im[:,0,:,:]= support_img[:,0,:,:]*support_mask 
            supprot_img_im[:,1,:,:]= support_img[:,1,:,:]*support_mask  
            supprot_img_im[:,2,:,:]= support_img[:,2,:,:]*support_mask  

            Feature_masking = self.extract_feats(support_img, self.backbone, self.feat_ids, self.bottleneck_ids, self.lids)
            Input_masking = self.extract_feats(supprot_img_im, self.backbone, self.feat_ids, self.bottleneck_ids, self.lids)

            Feature_masking = self.mask_feature(Feature_masking, support_mask.clone())

            for i in range(len(Feature_masking)):
                s_r = torch.where(Feature_masking[i]>0, Feature_masking[i],  Input_masking[i] )
                Feature_masking[i] = s_r
                
                
            query_feats = self.resize_feats(query_feats, self.stack_ids)           
            Hybrid_masking = self.resize_feats(Feature_masking, self.stack_ids)



For your convenience, we provide example files for HSNet, VAT and ASNet.


## Evaluation

Follow the testing directions for each method and use the pre-trained models with the above script.

HSNet-HM [Link](https://drive.google.com/drive/folders/1g8UJPSZDUeDlUFgaP_dlL0UFnWKq82uz?usp=sharing)
- Pascal-5 Benchmark with ResNet50
- Pascal-5 Benchmark with ResNet101
- COCO-20 Benchmark with ResNet50
- COCO-20 Benchmark with ResNet101
- FSS-1000 Benchmark with ResNet50
- FSS-1000 Benchmark with ResNet101

VAT-HM [Link](https://drive.google.com/drive/folders/1g8UJPSZDUeDlUFgaP_dlL0UFnWKq82uz?usp=sharing)

- Pascal-5 Benchmark with ResNet50 
- Pascal-5 Benchmark with ResNet101 
- COCO-20 Benchmark with ResNet50 
- FSS-1000 Benchmark with ResNet50 
- FSS-1000 Benchmark with ResNet101 

ASNet-HM [Link](https://drive.google.com/drive/folders/1g8UJPSZDUeDlUFgaP_dlL0UFnWKq82uz?usp=sharing)

- COCO-20 Benchmark with ResNet50 
- COCO-20 Benchmark with ResNet101

## Performance



## Visualization

<p align="middle">
    <img src="figure/comparison.png" width="600" height="350" />
</p>


## References

Our work is based on these models. (HSNet, VAT, and ASNet)

- [HSNet](https://github.com/juhongm999/hsnet) : Hypercorrelation Squeeze for Few-Shot Segmentation, ICCV 2021
- [VAT](https://github.com/Seokju-Cho/Volumetric-Aggregation-Transformer) : Cost Aggregation with 4D Convolutional Swin Transformer for Few-Shot Segmentation, ECCV 2022
- [ASNet](https://github.com/dahyun-kang/ifsl) : Integrative Few-Shot Learning for Classification and Segmentation, CVPR 2022

Thank you very much.

### BibTeX
If you find this research useful, please consider citing:

````BibTeX
@misc{moon2022hm,
      title={HM: Hybrid Masking for Few-Shot Segmentation}, 
      author={Seonghyeon Moon and Samuel S. Sohn and Honglu Zhou and Sejong Yoon and Vladimir Pavlovic and Muhammad Haris Khan and Mubbasir Kapadia},
      year={2022},
      eprint={2203.12826},
      archivePrefix={arXiv},
      primaryClass={cs.CV}
}
````
