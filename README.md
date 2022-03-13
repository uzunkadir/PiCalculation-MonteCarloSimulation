# PiCalculation-MonteCarloSimulation
 Pi Number Calculation with Monte Carlo Simulation and Plot
 
 <img src="images/img1.png" width="300">
 
````
import random
import matplotlib.pyplot as plt

#exact pi number
PI = 3.14159265358979323846264338327950288419716939937510

pointsX,   pointsY   = [], []  # coordinates of points 
accuracyX, accuracyY = [], []  # list of accuracy


fig, ax = plt.subplots(1,2,figsize=(16,8)) 
fig.suptitle('Pi Calculation with Monte Carlo Simulation', fontsize=16)

circle  = plt.Circle((0, 0), 1, color='blue')
points, = ax[0].plot(pointsX, pointsY,"o",color="black")
ax[0].add_patch(circle)


line, = ax[1].plot(accuracyX, accuracyY, "r-")
ax[1].axhline(y=100)


circle_points= 0
square_points= 0
  
for i in range(10**10):

    # create coordinate randomly
    rand_x= random.uniform(-1, 1)
    rand_y= random.uniform(-1, 1)
    pointsX.append(rand_x)
    pointsY.append(rand_y)
    
    # distance between circle's center and individual point
    origin_dist= rand_x**2 + rand_y**2
    
    # Checking if the point is inside the circle 
    if origin_dist<= 1:
        circle_points+= 1
    
    square_points+= 1
    
    # calculate pi
    pi = 4* circle_points/ square_points
    
    # calculate accuracy 
    accuracy = (1-abs(pi-PI)/PI)*100
    accuracyX.append(i)
    accuracyY.append(accuracy)
    
    ax[0].set_title("Points = {},  Estimated Pi Number: {:.10f}".format(i, pi),loc='left')
    points.set_xdata(pointsX)
    points.set_ydata(pointsY)

    ax[1].set_title("Accuracy: {:.10f}".format(accuracy),loc='left')
    line.set_xdata(accuracyX)
    line.set_ydata(accuracyY)


    ax[1].set_xlim(xmin=i-30, xmax=i+10)
    ax[1].set_ylim(ymin=min(accuracyY[max(0,i-30):i+1]), ymax=100.1)
    
    fig.canvas.draw()
    fig.canvas.flush_events()


print("Final Estimation of Pi=", pi)    

````
