---
layout: post
title:  "Black "
date:   2023-02-27 
categories: paint
---

> Some useful information on MATLAB plot

# Some color Code
- Deep Green :  #008000

# Functions

&ensp; 1. Point out specific point coordinates or text
```
text(AuNPs(idx1, 1)+7, AuNPs_max-0.03, sprintf('(%d, %.3f)', AuNPs(idx1, 1), AuNPs_max), "FontSize", 10); 
hold on;
```

&ensp; 2. Point out specific legend
```
legend([h(1) h(2) h(3) h(9) ], 'AuNPs (Control)', 'AuNPs+PBS', 'AuNPs@Ab+PBS', 'Spectral Peak');
```

&ensp; 3. Shadow a region in one figure

```
patch(x, y, uint8([222, 224, 227]));  or fill()
```




# Entire code examples

&ensp; 1. Example 1
```
a = zeros(130, 1);
b = zeros(130, 1);

figure(4);
for i = 1:1 :130
a(i, 1) = AuNPsPBS(130-i+1, 1);
b(i, 1) = 0.28;
end

x = cat(1, a, fliplr(AuNPsPBS(1:130, 1)));
y = cat(1, b, AuNPsPBS(1:130, 2));

patch(x, y, uint8([222, 224, 227])); hold on;
plot(AuNPsPBS(:, 1), AuNPsPBS(:, 2), Color='#0072BD', LineWidth=1.1);
% fill([AuNPsPBS(20:130, 1), fliplr(AuNPsPBS(20:130, 1))], [AuNPsPBS(20:130, 2), fliplr(AuNPsPBS(20:130, 2))], 'g');

xlabel('Wavelength (nm)');
ylabel('Absorbance');
title('AuNPs+PBS');
```

&ensp; 2. Example 2
```
%% Plot the figures with the max point in 1 plots
% Obtain the max point of 3 different solution

[AuNPs_max, idx1] = max(AuNPs(:, 2));
[AuNPsPBS_max, idx2] = max(AuNPsPBS(:, 2));
[AuNPsAbPBS_max, idx3] = max(AuNPsAbPBS(:, 2));

AuNPs_maxline = [[AuNPs(idx1, 1), 0]; [AuNPs(idx1, 1), AuNPs_max]];
AuNPsPBS_maxline = [[AuNPsPBS(idx2, 1), 0]; [AuNPsPBS(idx2, 1), AuNPsPBS_max]];
AuNPsAbPBS_maxline = [[AuNPsAbPBS(idx3, 1), 0]; [AuNPsAbPBS(idx3, 1), AuNPsAbPBS_max]];

% Plot the figures
figure(3);
h(1) = plot(AuNPs(:, 1), AuNPs(:, 2), LineWidth=1.1); hold on;
h(2) = plot(AuNPsPBS(:, 1), AuNPsPBS(:, 2), LineWidth=1.1); hold on;
h(3) = plot(AuNPsAbPBS(:, 1), AuNPsAbPBS(:, 2), LineWidth=1.1); hold on;

% Plot the corresponding max point line
h(4) = plot(AuNPs_maxline(:, 1), AuNPs_maxline(:, 2), '--');%, 'Color','black'); hold on;
h(5) = plot(AuNPsPBS_maxline(:, 1), AuNPsPBS_maxline(:, 2), '--');%, 'Color','black'); hold on;
h(6) = plot(AuNPsAbPBS_maxline(:, 1), AuNPsAbPBS_maxline(:, 2), '--');%, 'Color','black'); hold on;

% Plot the max points
h(7) = plot(AuNPs_maxline(2, 1), AuNPs_maxline(2, 2), '*r');%, 'Color','black'); hold on;
h(8) = plot(AuNPsPBS_maxline(2, 1), AuNPsPBS_maxline(2, 2), '*r');%, 'Color','black'); hold on;
h(9) = plot(AuNPsAbPBS_maxline(2, 1), AuNPsAbPBS_maxline(2, 2), '*r');%, 'Color','black'); hold on;

% Add the coordinates of the max points
text(AuNPs(idx1, 1)+7, AuNPs_max-0.03, sprintf('(%d, %.3f)', AuNPs(idx1, 1), AuNPs_max), "FontSize", 10); hold on;
text(AuNPsPBS(idx2, 1)+7, AuNPsPBS_max+0.02, sprintf('(%d, %.3f)', AuNPsPBS(idx2, 1), AuNPsPBS_max), "FontSize", 10); hold on;
text(AuNPsAbPBS(idx3, 1)+7, AuNPsAbPBS_max+0.02, sprintf('(%d, %.3f)', AuNPsAbPBS(idx3, 1), AuNPsAbPBS_max), "FontSize", 10); 

% Plot the setting
xlabel('Wavelength (nm)');
ylabel('Absorbance');
legend([h(1) h(2) h(3) h(9) ], 'AuNPs (Control)', 'AuNPs+PBS', 'AuNPs@Ab+PBS', 'Spectral Peak');
title('Absorption spectrum comparison');
set(figure(3), 'Position', [100, 100, 950, 450]);
set(figure(3), 'renderer', 'painters', 'name', 'Painters');

% Save the plots if has the savedir
saveas(figure(3), 'AbsorptionSpectrumComparison_all_v2.svg');
saveas(figure(3), 'AbsorptionSpectrumComparison_all_v2.fig');
```