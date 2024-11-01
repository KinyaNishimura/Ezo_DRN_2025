## Supplementary Information 2

#### Computation of bgPC scores for all individuals by projection of their Procrustes coordinates onto the bgPC tangent space using ‘Mathematica’

###### Designate a directory in which the data files and Mathematica programs are stored.

```
SetDirectory[NotebookDirectory[]];    (* Set directory in which the Data and this program are located  *)
```

###### Loading data

```
 (*  Procrustes coordinates data of All individuals    *)
AllSymGPAdata = Import["Symm.BE.GPA.AllInd.txt", "Table"]; 

(*  Mean Procrustes coordinates for each group of ‘treatment type’ by ‘population’    *)
GroupSymGPSdata = Import["Symm.BE.GPA.bg.txt", "Table"];   

(*  bgPC coefficients obtained from bgPCA based on mean Procrustes coordinates 
　　for each treatment type group by population. The calculations were performed 
　　in MorphoJ (Klingenberg 2011) on the data from "Symm.BE.GPA.AllInd.txt".      *)
bgCoeffsdata = Import["bgPCcoeffs.txt", "Table"];  

(*  ‘Head CS’ scorers of All individuals　 *)
HeadCSdata = Import["HeadCS.landsemiland.BE.txt",  "Table"];             
```

Reference: Klingenberg, C. P. (2011) MorphoJ: an integrated software package for geometric morphometrics. *Molecular Ecology Resources*, 11, 353–357.

###### Computation of bgPC scores for all individuals


```
AllIndSAymbgPCscorsList = 
  Table[(AllSymGPAdata[[2 ;;, 8 ;;]][[i]] - Mean[GroupSymGPSdata[[2 ;;, 7 ;;]]]), {i, 1, 332}] .bgCoeffsdata[[2 ;;, 2 ;;]];
AllIndSAymbgPCscorsList // Dimensions                    (*  Dimension check   *)
```

###### Data alignment


```
bgPCList = Table[ToExpression["bgPC" <> ToString[i]], {i, 14}];
result = List /@ HeadCSdata[[;; , 2]];
AllIndSymHeadCSbgPCscorsList =
  Join[
   Join[AllSymGPAdata[[;; , ;; 5]], result, 2],
   Join[{bgPCList}, AllIndSAymbgPCscorsList]
   , 2
   ];
AllIndSymHeadCSbgPCscorsList[[;; 5]] // TableForm
```

A part of the output data

```
Id					Location	...		bgPC1					bgPC2					...
EC-d14-01 	Erimo			...		0.0277112			0.00962554		...
EC-d14-02 	Erimo			...		0.0241041			0.0204539			...
...
```

