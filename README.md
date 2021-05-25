# Fuzzy-transitive-closure-computation
模糊传递闭包计算
```matlab
clear all;clc

X=[80 10 6 2;50 1 6 4;90 6 4 6;40 5 7 3;10 1 2 4];
for i=1:size(X,1)
    for j=1:size(X,2)
        newX(i,j)=X(i,j)/max(X(:,j));
    end
end
%%
% newX=newX';
%%
for i=1:size(newX,1)
    for j=1:size(newX,1)
        R(i,j)=mol(newX,i,j)/den(newX,i,j);
    end
end

%%
flag=1;
counter=0;
while flag
    R_old=R;
    R=FuzzySquare(R);
    if R_old==R
        flag=0;
    end
    counter=counter+1;
end

function y=mol(X,i,j)
    m=length(X(1,:));
    Sigma=0;
    for k=1:m
        Sigma=Sigma+X(i,k)*X(j,k);
    end
    y=Sigma;
end
function y=den(X,i,j)
    m=length(X(1,:));
    Sigma1=0;
    Sigma2=0;
    for k=1:m
        Sigma1=Sigma1+X(i,k)^2;
    end
    Sigma1=sqrt(Sigma1);
    for k=1:m
        Sigma2=Sigma2+X(j,k)^2;
    end
    Sigma2=sqrt(Sigma2);
    y=Sigma1*Sigma2;
end
function y=FuzzySquare(R)
    m=length(R);
    Rnew=size(R);
    for i=1:m
        for j=1:m
            for k=1:m
                tempmin(k)=min(R(i,k),R(k,j));
            end
        Rnew(i,j)=max(tempmin);
        end
    end
    y=Rnew;
end
```
