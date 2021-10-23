# Image classification using ensemble algorithms and zernike moments 
## Zernike moments
Zernike moments are features extracted by mapping the input image onto a complex set of Zernike polynomials.
Computing Zernike moments from an input image involves three steps. 
1.	The computation of the radial polynomials
2.	The computation of the Zernike basis functions
3.	The computation of the Zernike moments by mapping the image onto the Zernike basis functions [[1]](https://www.kaggle.com/smeschke/four-shapes).

## Dataset
To illustrate the use of zernike moments in shape recognition, we will use the Four Shapes dataset. This dataset contains 14970 samples of four classes: circles, squares, stars, triangles and the rotated version of each.. 
[link to the data](https://github.com/NoreddineDamane/Computer-Vision/blob/master/Feature%20Extraction%20Using%20Zernike%20Moments/images%2Bdoc/1-s2.0-S0031320306001166-main.pdf)

![](https://github.com/NoreddineDamane/Computer-Vision/blob/master/Image%20classification%20using%20ensemble%20algorithms%20and%20zernike%20moments/four%20shapes.PNG)

## Feature extraction
we computed the Zernike moments for the order and repetition (n, m) (n, m): ["(0, 0)", "(1, 1)", "(2, 0)", "(2, 2)", "(3, 1)", "(3, 3)", "(4, 0)", "(4, 2)", "(4, 4)", "(5, 1)", "(5, 3)", "(5, 5)", "(6, 0)", "(6, 2)", "(6, 4)", "(6, 6)" ,"(7, 1)", "(7, 3)", "(7, 5)", "(7, 7)"]

```python
m = []
n = []
N = np.arange(0 , 8)
M = np.arange(0 , 8)
for i in range (0,8):
    for j in range (0,8):
        if(((N[i] - abs(M[j])) % 2 == 0 ) and (abs(M[j]) <= N[i])): # n - |m| = pair et |m| <= n
            n.append(N[i])
            m.append(M[j])
}
zer_m = []
for c, idx in classes.items():
    class_folder = img_path + "{}/".format(c)
    for f in os.listdir(class_folder):
        k+=1
        
        fpath = class_folder + f
        sample = int(f.replace(".png", ""))
        img = cv.imread(fpath, cv.IMREAD_GRAYSCALE)
        img_ = np.logical_not(img)
        img_ = ~img_
        A_Z_m = []
        for i in range (0,20):
            [A, Phi] = Zernikmoment(img_,n[i],m[i])    # Call Zernikemoment fuction
            A_Z_m.append(round(A,4))
        A_Z_m = np.array(A_Z_m)
        A_Z_m = [idx] + A_Z_m.reshape((1, 20)).tolist()[0]
        zer_m.append(A_Z_m)

```


![](https://github.com/NoreddineDamane/Computer-Vision/blob/master/Image%20classification%20using%20ensemble%20algorithms%20and%20zernike%20moments/Feature.PNG)


## Classification using ensemble algorithms

### Decision tree
### Bagging
### Random forest