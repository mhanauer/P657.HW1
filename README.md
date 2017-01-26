# P657.HW1
%% Classify Using k-Nearest Neighbors
% Find the 10 nearest neighbors in |x| to each point in |y| using first the
% |'minkowski'| distance metric with a _p_ value of |5|, and then using the
% |'chebychev'| distance metric.
%%
% Load Fisher's iris data set

% Copyright 2015 The MathWorks, Inc.

load fisheriris
x = meas(:,3:4);
y = [5 1.45;6 2;2.75 .75];
%%
% Perform a |knnsearch| between |x| and the query points in |y|,
% using first Minkowski then Chebychev distance metrics.
[n,d]=knnsearch(x,y,'k',10,'distance','minkowski','p',5);
[ncb,dcb] = knnsearch(x,y,'k',10,...
   'distance','chebychev');
%%
% Visualize the results of the two different nearest neighbors searches.
% Plot the training data. Plot an X for the query points. Use circles to
% denote the Minkowski nearest neighbors. Use pentagrams to denote the
% Chebychev nearest neighbors.
gscatter(x(:,1),x(:,2),species)
line(y(:,1),y(:,2),'marker','x','color','k',...
   'markersize',10,'linewidth',2,'linestyle','none')
line(x(n,1),x(n,2),'color',[.5 .5 .5],'marker','o',...
   'linestyle','none','markersize',10)
line(x(ncb,1),x(ncb,2),'color',[.5 .5 .5],'marker','p',...
   'linestyle','none','markersize',10)
legend('setosa','versicolor','virginica','query point',...
'minkowski','chebychev','Location','best')
