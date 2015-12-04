---
event: '2015 Brainhack Americas (MX)'

title:  'NeuroView: a customizable browser-base utility'

author:

- initials: ASH
  surname: Sólon Heinsfeld
  firstname: Anibal
  email: anibalsolon@gmail.com
  affiliation: pucrs

- initials: ARF
  surname: Rosa Franco
  firstname: Alexandre
  email: alexandre.franco@pucrs.br
  affiliation: pucrs

- initials: AB
  surname: Buchweitz
  firstname: Augusto
  email: augusto.buchweitz@pucrs.br
  affiliation: pucrs

- initials: FM
  surname: Meneguzzi
  firstname: Felipe
  email: felipe.meneguzzi@pucrs.br
  affiliation: pucrs

affiliations:

- id: pucrs
  orgname: 'PUCRS'
  street: Av. Ipiranga, 6681
  postcode: 90619-900
  city: Porto Alegre
  state: Rio Grande do Sul
  country: Brazil

url: https://github.com/lsa-pucrs/neuroview

coi: None

acknow: The authors would like to thank the organizers and attendees of Brainhack MX and the developers of AFNI.

contrib: ASH wrote the software, and ASH, FM, ARF, and AB wrote the report.

bibliography: brainhack-report

gigascience-ref: REFXXX
...

#Introduction
The amount of data gathered from fMRI scans, specially by its dimensionality, brings challenges to neuroscience when it comes to data analysis and visualization.
Different tools has been developed to oppose these challenges, but studies might have slight differences on analysis, that are not covered by such tools.

#Approach
The goal of this Brainhack project build a flexible utility to analyse fMRI experimental results.
This utility is called NeuroView.
NeuroView allows researchers to extend the visualizations to their context: every visual behavior or interactions of this tool is customizable.
We implemented NeuroView to work in Web-browsers, using JavaScript and the libraries D3.js and jQuery.

#Results
Three tools within NeuroView have been created to best analyze research results: CC200 search, SVM coeffs and Connectivity matrix.
Each tool is used to aid the analysis of results in Machine Learning tasks.
Each of these tools are described below in detail.

## \texttt{CC200 search}:
In this tool, we allow the user to find atlas regions (e.g. Left Putamen from Harvard-Oxford subcortical structural atlas) mapped to a specific parcellation.
As as initial approach, the CC200 \cite{Craddock2012} parcellation method was used, since our analysis uses data from functional MRI.
<!-- Thus, CC200 search tool helps us to identify which CC200's ROIs belongs to which atlas regions. -->
Since we parcellate our data into CC200's ROIs in most of our studies, the identification of atlas regions became necessary to compare with results found in the literature.
The search can be performed in two manners: it is possible to search for a atlas region (e.g. Putamen) and retrieve which parcels are included in this region, and it is possible to click a ROI in NeuroView to retrieve which atlas regions include the specific parcel.

## \texttt{SVM coeffs}:
For the second tool, we created a user interface to identify the ROIs that contribute to the classification in a Support Vector Machine.
The classification method uses task-based fMRI features to identify good and poor readers \cite{Salles2013}.
Given a list of most relevant features, as shown in Figure \ref{fig:svm_coeffs}, we can show the features' parcel in NeuroView and identify to which atlas regions this parcel belongs to.

\begin{figure}[ht]
\centering
\includegraphics[width=0.45\textwidth]{figs/svm_coeffs.png}
\caption{SVM coeffs tool showing the most relevant feature in a classification task.}
\label{fig:svm_coeffs}
\end{figure}

## \texttt{Connectivity matrix}:
In the third study case, NeuroView was customized to interact with a connectivity chord plot.
This plot contains each CC200 parcel and chords that represent the connectivity between these parcels.
Since we use the connectivity matrix as features for our deep learning method, we need to check which feature (i.e. the correlation between two parcels)
most contributes to the classification.
After thresholding 17995 features, we retrieve 10 features that are more relevant in our analysis, as shown in Figure \ref{fig:deeplearning}.
In the chord plot, a red chord indicates that two regions are correlated, and a blue chord indicates that two regions are anti-correlated.
By clicking a chord, NeuroView highlights the regions that are connected by this chord.
Thus, highlighted regions are correlated (or anti-correlated) given the chord color.

\begin{figure}[ht]
\centering
\includegraphics[width=0.45\textwidth]{figs/deeplearning.png}
\caption{Deep learning.}
\label{fig:deeplearning}
\end{figure}

# Conclusion

This is a initial version of a browser-based neuroimage viewer.
The main focus is to develop an embeddable viewer, instead of a standalone desktop software.
By doing so, research results can be presented on interactive views, enriching their analysis and interpretation.
In our case study, NeuroView facilitate quick evaluation of features for machine learning algorithms, and promote discussion about them, since the results were enlightened among researchers.

As further work, we aim to directly load Nifti images at client-side and support some AFNI's features, such as voxel clustering.