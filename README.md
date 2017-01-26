function [neighborIds neighborDistances] = kNearestNeighbors(dataMatrix, queryMatrix, k)
% So the name is kNearestNeighbors, outputs are neighborIds neighborDistances 
% and the inputs are the things inside arguments
% So we need run this function first to create it
%--------------------------------------------------------------------------
% Program to find the k - nearest neighbors (kNN) within a set of points. 
% Distance metric used: Euclidean distance
% 
% Usage:
% [neighbors distances] = kNearestNeighbors(dataMatrix, queryMatrix, k);
% dataMatrix  (N x D) - N vectors with dimensionality D (within which we search for the nearest neighbors)
% queryMatrix (M x D) - M query vectors with dimensionality D
% k           (1 x 1) - Number of nearest neighbors desired
% 
% Example:
% a = [1 1; 2 2; 3 2; 4 4; 5 6];
% b = [1 1; 2 1; 6 2];
% [neighbors distances] = kNearestNeighbors(a,b,2);
% Why are neighbors and distances in brackets aren't you assigned this to
% the kNearestNeighbors function
% Output:
% neighbors =
%      1     2
%      1     2
%      4     3
% 
% distances =
%          0    1.4142
%     1.0000    1.0000
%     2.8284    3.0000
%--------------------------------------------------------------------------

neighborIds = zeros(size(queryMatrix,1),k);
% Creating a matrix of zeros for potential cluster ID's
neighborDistances = neighborIds;
% Reassinging the name to neighborDistances
numDataVectors = size(dataMatrix,1);
% This is creating an empty vector 
% Size is equal to the dataMatrix and then creates one of them
% Data Matrix is equal to the original data
numQueryVectors = size(queryMatrix,1);
% numQueryVectors
for i=1:numQueryVectors
    dist = sum((repmat(queryMatrix(i,:),numDataVectors,1)-dataMatrix).^2,2);
    % Here is where I would transform distance into the weighted distance
    [sortval, sortpos] = sort(dist,'ascend');
    neighborIds(i,:) = sortpos(1:k);
    neighborDistances(i,:) = sqrt(sortval(1:k));
end
