# __Emoprox II__

__Project path:__ `/data/bswift-1/Pessoa_Lab/eCON`

# Data
- Brain data
    - Dicom files: `dicomdir`
    - Raw nifti files: `dataset/raw`
    - Preprocessed data:
        - smooth: `dataset/preproc2/CON???/func/ICA_AROMA/CON???_EP_TR_MNI_2mm_SI_denoised.nii.gz`
        - unsmooth: `dataset/preproc2/CON???/func/ICA_AROMA/CON???_EP_TR_MNI_2mm_I_denoised.nii.gz`
- Raw behavioral data
    - `STAIscores/fMRI_CON.xlsx`: data collection log, detailed STAI scores
    - `STAIscores/scores.xlsx`: summarized STAI scores
    
# Regressors
Two set of regressors were created for two different analyses: Parametirc and Categorical.
- __Parametric:__  
For parametirc analysis, circles' proximity is modeled parametrically. Detailed information of regressors creation can be found in `documentation/scripts`. Read the following notebooks in the given order to understand regressor creation process:
 - `1-StimulusExtraction.ipynb`
 - `2-TimingExtraction.ipynb`
 - `3-TimingAlignment.ipynb`
 - `4-InteractionCreation.ipynb`
 - `5-ConvolveDecimate.ipynb`
 - `6-SaveRegsOnsets.ipynb`
 
- __Categorical:__  
For categorical analysis, cricles' proximity was categorized into three levels: _nearest_, _near_, and _far_. For eaxmple, if 0 and 1 are minimum and maximum possible proximity values, then _nearest_ is the period when the circles are in a proximity range of (0.66-0.99), _near_ is the period when the circles are in the proximity range of (0.33-0.66), and _far_ is when circles are in the range of (0-0.33). Each proximity category is modeled as a block regressor. Code to create these regressors: `make_regs_cat/SaveRegsAllSubj.ipynb` 

Categorical analysis was used as the final analysis method. Results in the controllabilty paper were generated using this method. 

# Analyses 
Analysis scripts for results presented in the controllabilty paper:
## First Level Analysis
### Voxelwise
- Physical shock response 
    - Assumed shape analysis 
        - uncontrollable participants: `scripts/tmp_preproc2/voxelwise/uncon_shock_MR_noProx.sh`  
        - controllable participants: `scripts/tmp_preproc2/voxelwise/con_shock_MR_noProx.sh`
    - Unassumed shape analysis
        - uncontrollable participants: `scripts/tmp_preproc2/voxelwise/uncon_shock_deconv_noProx.sh`  
        - controllable participants: `scripts/tmp_preproc2/voxelwise/con_shock_deconv_noProx.sh`
        
### ROI Analysis
- Physical shock response
    - Assumed shape analysis
        - uncontrollable participants: `scripts/tmp_preproc2/ROI_analysis/buttonPress/shock_MR/uncon_shock_MR.sh`
        - controllable participants: `scripts/tmp_preproc2/ROI_analysis/buttonPress/shock_MR/con_shock_MR.sh`
    - Unassumed shape analysis
        - uncontrollable participants: `scripts/tmp_preproc2/ROI_analysis/buttonPress/shock_deconv/uncon_shock_deconv.sh`
        - controllable participants: `scripts/tmp_preproc2/ROI_analysis/buttonPress/shock_deconv/con_shock_deconv.sh`
    
        
        
## Group Level Analysis
### Voxelwise
- Physical shock response (uncontrol vs. control): `scripts/tmp_preproc2/voxelwise/Group_Analysis_ShockUncensored_UnconVsCon.sh`
### ROI analysis
- Physical shock response (uncontrol vs. control): BML analysis was carried out instead of typical group analysis. Further documentation can be found in the [`controllability_paper/README.md`](https://github.com/LCE-UMD/controllabilty_paper/blob/master/README.md)