Modeling-Customer-Relationships-as-Markov-Chains
================================================

Code made in R-Studio is based on work done by Pfeifer &amp; Carraway (2000) with paper title 'Modeling Customer Relationships as Markov Chains'

#Modeling Lifetime Value of Customer by using Markov Chains
#Theory as given in Pfeifer & Carraway (2000) - Modeling Customer Relationships as Markov Chains

#We are going to contruct a 5x5 one-step transition probability matrix with values:
#p_1 = 0.3
#p_2 = 0.2
#p_3 = 0.15
#p_4 = 0.05

MatrixP = matrix(
c(0.3,0.2,0.15,0.05,0,0.7,0,0,0,0,0,0.8,0,0,0,0,0,0.85,0,0,0,0,0,0.95,1),
nrow=5,
ncol=5)
MatrixP

#Now we need to construct the column vector for the economic evaluation of the relationship
#We will create a 5x1 column vector R, setting NC = £40 annd M = £4 :

VectorR = matrix(
c(36,-4,-4,-4,0),
nrow=5,
ncol=1)
VectorR

#We now how to times the one-step transition Matrix P by our (1+d)^-1
#In this simulation, I will set d = 0.2

#Now we must define each vector for lifetime value in each period 
#We must to times the probability matrix by (1+d)^-1, in this simulation, I will set d = 0.2
#The Value of a customer * The Economic Evaluation (Column Vector R)


V1 = MatrixP
V1 = V1 %*% VectorR
V1

V2 = ((MatrixP %*% MatrixP) * 0.8333^2)
V2 = V2 %*% VectorR
V2

V3 = ((MatrixP %*% MatrixP %*% MatrixP) * 0.8333^3)
V3 = V3 %*% VectorR
V3

V4 = ((MatrixP %*% MatrixP %*% MatrixP %*% MatrixP %*% MatrixP) * 0.8333^4)
V4 = V4 %*% VectorR
V4

#Sum of the previous four vectors is therefore:

Value = (V1 + V2 + V3 + V4)
Value

#If we had got a negative entry in Column Vector 'Value', we would have set probability
# p_4 equal to 0 and re-run the simulation. If we had got antoher negative entry, we would 
# set p_3 equal to 0 and re-run the simulation, and continued until no negative entries
# were left in the Column Vector 'Value'.
