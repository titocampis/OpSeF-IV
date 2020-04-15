## About OpSeF IV

OpSeF has been primarily developed for staff image analysts with solid knowledge in image analysis, thorough understating of the principles of machine learning, and ideally basic skills in Python. 

The analysis pipeline consists of four principal sets of functions to *import and reshape* the data, to *pre-process* it, to *segment* objects, and to *analyze and classify* results. 



<img src="./Demo_Notebooks/Figures_Demo/Fig_M1.jpg" alt = "Paper Fig M1" style = "width: 500px;"/>

Currently, OpSeF can process individual tiff-files and the Leica “.lif” container file format. During *import and reshape,* the following options are available for tiff-input: *tile* in 2D and 3D, *scale*, and make *sub-stacks* . For lif-files, only the make *sub-stacks* option is supported. 

Pre-processing is mainly based on scikit-image. It consists of a linear pipeline: 

<img src="./Demo_Notebooks/Figures_Demo/Fig_M3.jpg" alt = "Paper Fig M3" style = "width: =800px;"/>

Images are filtered in 2D, background is removed, and then stacks are projected. Next, the following optional pre-processing operations might be performed: histogram adjustment, edge enhancement, and inversion of images. 

Segmentation in cooperates the pre-trained U-Net implementation used in Cellprofiler 3.0, the StarDist 2D model and Cellpose. 

Importantly, OpSeF is designed such that parameters for pre-processing and selection of the ideal model for segmentation are one functional unit. 

<img src="./Demo_Notebooks/Figures_Demo/Fig_M4.jpg" alt = "Paper Fig M4" style = "width: 500px;"/>

Left panel: Illustration of a processing pipeline, in which three different models are applied to data generated by four different pre-processing pipelines each. Right panel: Resulting images are classified into results that are correct; suffer from under- or over-segmentation or fail to detect objects. 



## How to get started:

1) Clone repository

2) Download data from https://owncloud.gwdg.de/index.php/s/nSUqVXkkfUDPG5b

3) Setup environment

4) Execute OpSeF_IV_Configure_001.ipynb (only once after installation)

5) Open any demo notebook

6) Define the path, where you put the data (see QuickStart.pdf) and execute notebook

7) Copy this file-path of the .pkl file (see QuickStart.pdf)

8) Open OpSeF_IV_Run_001.ipynb and point the variable file_path to the .pkl file generated in 7) 

​     (see QuickStart.pdf)

Link to QuickStart.pdf: 

[QuickStart.pdf](./Documentation/Quick_Start_OpSeF.pdf)



## Advanced Use:

#### Define your own project:

1) Copy an existing Demo Notebook

2) Organize all input data in one folder

*using .lif as input:*

​	root/myimage_container.lif

*using .tif as input:*

​	root/tiff/myimage1.tif (in case this folder is the direct input to the pre-processing pipeline)

​	root/tiff/myimage2.tif ...

​	root/tiff_raw_2D/myimage1.tif (if you want to make patches in 2D)

​	root/tiff_to_split/myimage1.tif (if you want ONLY create substacks, no binning or creation of patches) 

​	root/tiff_raw/myimage1.tif (for all pipelines that start with patching or binning and use stacks)

3) Point Demo Notebook to this folder & give notebook a common name:

```python
input_def["root"] = "/home/trasse/Desktop/MLTestData/leaves"
input_def["dataset"] = "leaves"
```

4) Define input type

```python
input_def["input_type"] = ".tif"
```

5) Define first test run (give it a Run_ID, define pre-processing & which model to test)

```python
run_def["run_ID"] = "001"  # give each run a new ID 
                           #(unless you want to overwrite the old data)

run_def["pre_list"] = [["Median",3,50,"Max",False,run_def["clahe_prm"],"no",False],
                       ["Median",3,50,"Max",True,run_def["clahe_prm"],"no",False],
                       ["Median",3,50,"Max",False,run_def["clahe_prm"],"sobel",False],
                       ["Median",3,50,"Max",False,run_def["clahe_prm"],"no",True]]

# For Cellpose
run_def["rescale_list"] = [0.2,0.4,0.6] # run1

# Define model
run_def["ModelType"] = ["CP_nuclei","CP_cyto","SD_2D_dsb2018","UNet_CP001"] # run1
```

6) Execute Run in OpSeF_IV_Run_001.ipynb (as described for the demo notebooks)



### Further Information:

Documentation of naming schemes used: 

guide_to_folder_structure_and_file_naming.txt

Documentation of main variables used: 

guide_to_variables.txt

Further Questions:

see FAQ :

[FAQ](./Documentation/FAQ.pdf)

## Common Issues



## How to Contribute

OpSeF-IV currently contains four pre-trained model. Thus, it is is currently more a prove of concept.

Many similar approaches are "developer to end user".

The ideal behind OpSeF is a from staff image analyst to staff project.

It will reach it's full potential only by being transformed into a community project.

Thus, if you lack a feature, please try to add it yourself.

Please find the current to-do list here: 

[To Do](./To_Do/to_do.txt)

Please consider to solve one of these tasks.

If you train new model, please make them available in OpSeF.

Hopefully, we could together publish the OpSeF-XL update 

(with 40 pre-trained model instead of 4) within a year.

Please contribute new Demo_Notebooks.

Please contribute teaching material.

If you get stuck please e-mail me & I will try to troubleshoot.

Then please consider to multiply you knowledge by volunteering to help other analysts in using and developing OpSeF.  



