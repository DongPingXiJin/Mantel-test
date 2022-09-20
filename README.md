 Matel test based on R language visualization
 
##Mantel code and test files (A.csv, B.csv) have been uploaded today.（2022/09/20）#####

Note: If you want to apply this code. First, download R studio and R on your computer.Then，you should install three packages,which was dplyr ，linKEt and ggplot2.

Mantel test can analyze the correlation of two matrices (matrix A and matrix B).If you want to know more about mantel analysis, you can read this paper: https://doi.org/10.1111/2041-210x.12018.

eg.
![image](https://github.com/DongPingXiJin/Mantel-test-use-LinKet-/blob/main/images/Mantel%20test.jpg)

To draw such a picture, you need to first analyze the composition of the picture.
![image](https://github.com/DongPingXiJin/Mantel-test-use-LinKet-/blob/main/images/1663642080039.png)
![image](https://github.com/DongPingXiJin/Mantel-test-use-LinKet-/blob/main/images/1663646346589.png)

Before using, you need to save the two matrix data in. csv format. And specify which matrix is used for correlation analysis thermodynamic diagram.

Several program descriptions:

                               spec_select = list(Y1 = 1:7,
			       
                                           Y2 = 8:18,
					   
                                           Y3 = 19:37,
					   
                                           Y4 = 38:44
					   
                                           )) 

The matrix A is classified according to the columns, where 1-7 is divided into the first category, 8-18 into the second category, and so on. Later, you can flexibly apply and modify according to your own data. For example, if you want to divide the data into four categories with only four columns, you can write: 

                                   spec_select = list(Y1 = 1,
				   
                                           Y2 = 2,
					   
                                           Y3 = 3,
					   
                                           Y4 = 4
					   
                                           )) 
					   
                                           
Analyze mantel test results, classify r and p values and define labels：

######################################################################

                 mutate(rd = cut(r, breaks = c(-Inf, 0.2, 0.4, Inf),
 
                  labels = c("< 0.2", "0.2 - 0.4", ">= 0.4")),
                  
         pd = cut(p, breaks = c(-Inf, 0.01, 0.05, Inf),
         
                  labels = c("< 0.01", "0.01 - 0.05", ">= 0.05")))
                 
#######################################################################

Draw thermodynamic diagram：
######################################################################

          qcorrplot(correlate(env), 

          type = "lower",    //Display the lower triangle thermodynamic diagram, which can be modified to "upper" to display the upper triangle thermodynamic diagram
          
          diag = FALSE,     // Don't show diagonal
          
          ) +
          
         geom_square()
  
######################################################################

Modify the color and size of the mantel test connection point：

#####################################################################

              geom_couple(aes(colour = pd, size = rd),data = mantel01, curvature = 0.1,

              node.colour = c("blue", "blue"),
              
              node.fill = c("grey", "grey"),
              
              node.size = c(3.5, 2.5),
              
              )
              
####################################################################

Modify the color matching and legend of the thermal diagram：

#####################################################################	

                      scale_fill_gradientn(colours = RColorBrewer::brewer.pal(11, "RdBu"),

                       limits = c(-1, 1),
											 
                       breaks = seq(-1,1,0.5))
											 
#####################################################################	

Set mantel test connection line

####################################################################   

	     scale_size_manual(values = c(0.5, 1, 1.5, 2)) +
	     
             scale_colour_manual(values = color_pal(3)) +
	     
####################################################################

