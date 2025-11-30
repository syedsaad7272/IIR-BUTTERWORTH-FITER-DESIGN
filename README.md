
# EXP 3 : IIR-BUTTERWORTH-FITER-DESIGN
## SYED SAAD (212223060283)

## AIM: 

 To design an IIR Butterworth filter  using SCILAB. 

## APPARATUS REQUIRED: 
PC installed with SCILAB. 

## PROGRAM (LPF): 
~~~
clc ;
close ;
wp=input('Enter the pass band frequency (Radians )= ' );
ws=input('Enter the stop band frequency (Radians )= ' );
alphap=input( ' Enter the pass band attenuation (dB)=' );
alphas=input( ' Enter the stop band attenuation(dB)=' );
T=input('Enter the Value of sampling Time=');
//Pre warping- Bilinear Transformation
omegap=(2/T)*tan(wp/2);
disp(omegap,'omegap=');
omegas=(2/T)*tan(ws/2);
disp(omegas,'omegas=');
//Order of the filter
N=log10(((10^(0.1*alphas))-1)/((10^(0.1*alphap))-1))/(2*log10(omegas/omegap));
disp(N,'N=');
N=ceil(N);
disp(N,'Round off value of N=');
//Cut off frequency
omegac=omegap/(((10^(0.1*alphap)) -1)^(1/(2* N)));
disp(omegac,'omegac=');
disp('Normalised Analog LPF Transfer function H(S)=');
hs_Normalised = analpf(N,'butt',[0,0],1);
disp(hs_Normalised);
disp('Analog LPF Transfer function H(S)=');
hs= analpf(N,'butt',[0,0],omegac);
disp(hs);
z=poly(0,'z');//Defining variable z
Hz=horner(hs,(2/ T)*((z -1)/(z+1)))// Bilinear Transformation
disp('Digital LPF Transfer function H(Z)=');
disp(Hz);
HW=frmag(Hz,512); // Frequency response
w=0:%pi/511:%pi ;
plot(w/%pi,abs(HW));
xlabel(' Normalized Digital Frequency w');
ylabel('Magnitude ');
title(' Frequency Response of Butterworth IIR LPF');

~~~
## CALCULATION:
<img width="1919" height="1072" alt="image" src="https://github.com/user-attachments/assets/38ba0688-4b17-4fcf-b84d-86c7685a2062" />
<img width="1919" height="380" alt="image" src="https://github.com/user-attachments/assets/15aa2044-b758-4bc1-acbf-0ed8d0f0e5b4" />


## OUTPUT (LPF) : 
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/0cfffad8-42a6-4bf3-9e99-46002e83534a" />


## PROGRAM (HPF): 
~~~
clc;
clear;
close;

// User inputs
wp = input('Enter the pass band frequency (Radians )= ');
ws = input('Enter the stop band frequency (Radians )= ');
alphap = input('Enter the pass band attenuation (dB)= ');
alphas = input('Enter the stop band attenuation (dB)= ');
T = input('Enter the Value of sampling Time=');

// Pre-warping
omegap = (2/T)*tan(wp/2);
disp(omegap, 'omegap=');
omegas = (2/T)*tan(ws/2);
disp(omegas, 'omegas=');

// Order of the filter
N = log10(((10^(0.1*alphas))-1)/((10^(0.1*alphap))-1))/(2*log10(omegap/omegas));
disp(N, 'N=');
N = ceil(N);
disp(N, 'Round off value of N=');

// Cutoff frequency (for high-pass, based on stopband ratio)
omegac = omegas/(((10^(0.1*alphas)) -1)^(1/(2* N)));
disp(omegac, 'omegac=');

// Normalized Analog LPF
disp('Normalized Analog LPF Transfer function H(s)=');
hs_Normalised = analpf(N,'butt',[0,0],1);
disp(hs_Normalised);

// Actual Analog LPF
disp('Analog LPF Transfer function H(s)=');
hs = analpf(N,'butt',[0,0],omegac);
disp(hs);

// ---------- LPF to HPF Transformation ----------
s = poly(0,'s');
hs_hp = horner(hs, (omegac^2)/s);   // low-pass → high-pass transform

disp('Analog HPF Transfer function H(s)=');
disp(hs_hp);

// ---------- Bilinear Transformation ----------
z = poly(0,'z');
Hz = horner(hs_hp, (2/T)*((z - 1)/(z + 1)));

disp('Digital HPF Transfer function H(z)=');
disp(Hz);

// ---------- Frequency Response ----------
HW = frmag(Hz,512);
w = 0:%pi/511:%pi;

plot(w/%pi, abs(HW));
xlabel('Normalized Digital Frequency (×π rad/sample)');
ylabel('Magnitude');
title('Frequency Response of Butterworth IIR High-pass Filter');
xgrid();
~~~


## OUTPUT (HPF) : 
<img width="945" height="896" alt="image" src="https://github.com/user-attachments/assets/2d71edf6-0e94-4462-87a3-2c218cf0bec1" />


## RESULT: 
Thus, design of Butterworth IIR filter waveforms were plotted and output was
verified.
