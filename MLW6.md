[Home](/README.md)


### Refining the TDSE PIB 
1. The TDSE for the PIB with a linear commbination of the first two values

'''

function TDSEa(n)
hbar=1;
m=1; % mass of electron
l=1; % length of box 0.5 nm (written in meters)
pts=300; % number of discretized points

%discretize space
x=linspace(0,l,pts)'; % discretized space
dx=x(2)-x(1);

% barrier parameters
barht=1E6; %bar height on potential matrix
w=3; % number of points within infinite wall

c=-(hbar.^2)/(2.*m); % constant in kinetic energy operator
D=(1/((dx)^2)).*(-2*eye(pts)+diag(ones(pts-1,1),-1)+diag(ones(pts-1,1),1)); % second derivative matrix
T=c.*D;

Vvec=zeros(pts,1);
Vvec([1:w,(end-(w-1)):end])=barht;
V=diag(Vvec);

H=T+V;

[vecs,vals]=eig(H); % determining eigenvectors and eigenvalues
[srtvecs,srtvals]=eigsort(vecs,vals); % sorting eigenvalues in ascending order

EtoX=srtvecs; % change from energy basis to position basis
XtoE=inv(srtvecs); % change from position basis to energy basis

psiE=zeros(pts,1); % vector of all zeros
psiE([1 2])=1; % change position 1,2 in vector to 1
psiX=EtoX*psiE;

%How to shift on displayng graph
% sc=100; 
% srtvecs=sc*srtvecs;
% v=diag(srtvals); % vector of sorted eigenvalues
% repvals=(ones(pts,1))*v';
% shiftvecs=srtvecs+repvals;
    v=diag(srtvals);
    repvals=(ones(pts,1))*v';
    
    %New Content
t=0; dt=0.1;
for k=1:100
    psiEt=psiE.*exp(-i*v*t/hbar);
    psiEt=psiEt./norm(psiEt); % normalize vector of psiE (dependent on time)

    psiXt=EtoX*psiEt;
    psiXt=psiXt./norm(psiXt); % normalize vector of psiX (dependent on time)
    expv=real(psiXt' * (x.*psiXt));  %Expectation Value
    
%     rpsiEt=psiE.*(diag(srtvals)*t/hbar); % real psiEt
%     rpsiXt=EtoX*rpsiEt; % real psiXt
%     rpsiXt=rpsiXt./norm(rpsiXt); % normalized and real psiXt used for the probability density

%        expX=dot(rpsiXt,rpsiXt)/2;
    
    figure(1)
        subplot(2,2,1)
        JA_plot3(x,psiXt)
        
        subplot(2,2,2)
        JA_plot3(diag(srtvals),psiEt)
        
        subplot(2,2,[3,4])
        plot(x,abs(psiXt).^2) % the probability density
        axis([-inf inf 0 5E-2])
        plot(v,snrps; xt)(:,1).expX,'r.*';  %expectation value indicator
        %plot(x,snrpsiXt(:,1),x,expX)  
        %axis([-inf inf 0 .1])
        drawnow
    
    t=t+dt;
end

end

function [ srtvecs,srtvals ] = eigsort( vecs,vals ) % acending order eigenvectors and eigenvalues
d=diag(vals);
[dsort,ord]=sort(d);
srtvecs=vecs(:,ord);
srtvals=diag(dsort);

end

function JA_plot3(basisaxis,psi);
%% Plot complex valued vectors as 3D plots. The complex plane forms the
%% backdrop for the plot and the eigenvalue axis
%% projects out from plane.
        
        s = 1; % 1/s defines the fraction of eigenvalue axis that is displayed
    % For more information see notes from 2/8/18    
    % Begin by grabbing the real and imaginary parts of the vector psi,
    % defining the length of the "space" axis, and defining a vector of 
    % zeros that serve as the axis relative to which psi is plotted.
        realpart = real(psi);   % extract the real part of psi
        imagpart = imag(psi);   % extract the imaginary part of psi
        n = length(basisaxis);  % number of points in each vector
        bsl = zeros(n,1);       % define baseline as n zeros

    % Create a three dimensional stem plot. The bases of the stems are 
    % placed at the baseline "bsl" and the heads of the stems are displaced
    % from the baseline by the real and imaginary values of each vector
    % element
        plot3(...
          [basisaxis basisaxis]',[bsl realpart]',[bsl imagpart]','k',... % black stems
          basisaxis,realpart,imagpart,'b.') % stem heads as blue dots
        axis([min(basisaxis) max(basisaxis)/s -1 1  -1 1]); % set axis limits
        pbaspect([3,1,1])   % fix aspect ratio of 3D plot
        view([70,10])       % define the view angle
grid on             % turn on the grid
end 

'''