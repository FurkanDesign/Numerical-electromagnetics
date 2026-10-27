# Numerical-electromagnetics
Numerical evaluation and error analysis of the 2D Laplace equation in a rectangular pipe using MATLAB.

% =========================================================================
% Potential Distribution Inside a Rectangular Tube and Percentage Error Analysis
% =========================================================================
clear; clc; close all;

% --- 1. PARAMETER AND GRID (MESH) DEFINITION ---
a = 1.0;  % Box width (x-axis)
b = 1.0;  % Box height (y-axis)
V0 = 1.0; % Potential of the top wall

% Create a grid with 100 x 100 points
nx = 100;
ny = 100;
x = linspace(0, a, nx);
y = linspace(0, b, ny);
[X, Y] = meshgrid(x, y);

% --- 2. POTENTIAL DISTRIBUTION CALCULATION (N = 50 TERMS) ---
N_terms_plot = 50;
Phi = zeros(size(X));

for i = 1:N_terms_plot
    n = 2*i - 1; % Odd integers only (1, 3, 5, 7, ...)
    
    coefficient = (4 * V0) / (n * pi * sinh(n * pi * b / a));
    x_component = sin(n * pi * X / a);
    y_component = sinh(n * pi * Y / a);
    
    Phi = Phi + coefficient * x_component .* y_component;
end

% --- 3. PLOT OF THE POTENTIAL DISTRIBUTION ---
figure('Name', 'Potential Distribution', 'Color', 'w');
contourf(X, Y, Phi, 50, 'LineColor', 'none');
colormap(jet);
colorbar;
title('Potential Distribution Inside a Rectangular Tube \varphi(x,y)');
xlabel('x');
ylabel('y');
axis square;
set(gca, 'Color', 'w'); % Ensure the axes background is white
grid on;

% --- 4. PERCENTAGE ERROR CALCULATION AND PLOT ---
% Reference point (center of the box: x = 0.5, y = 0.5)
x_ref = 0.5;
y_ref = 0.5;

% 50 terms are more than sufficient for machine precision.
% Larger values (e.g., 500) may cause overflow, resulting in Inf/Inf = NaN.
N_exact = 50;
phi_exact = 0;

for i = 1:N_exact
    n = 2*i - 1;
    coefficient = (4 * V0) / (n * pi * sinh(n * pi * b / a));
    phi_exact = phi_exact + coefficient * ...
        sin(n * pi * x_ref / a) * sinh(n * pi * y_ref / a);
end

% Calculate the error for different numbers of terms (N = 1 to 20)
max_N_test = 20;
percentage_errors = zeros(1, max_N_test);

for N = 1:max_N_test
    phi_N = 0;
    
    for i = 1:N
        n = 2*i - 1;
        coefficient = (4 * V0) / (n * pi * sinh(n * pi * b / a));
        phi_N = phi_N + coefficient * ...
            sin(n * pi * x_ref / a) * sinh(n * pi * y_ref / a);
    end
    
    percentage_errors(N) = abs((phi_exact - phi_N) / phi_exact) * 100;
end

% Plot the percentage error
figure('Name', 'Percentage Error', 'Color', 'w');
plot(1:max_N_test, percentage_errors, '-o', ...
    'LineWidth', 1.5, ...
    'MarkerSize', 6, ...
    'MarkerFaceColor', 'b', ...
    'Color', 'b');

title('Percentage Error vs. Number of Terms (Reference Point: x = 0.5, y = 0.5)');
xlabel('Number of Terms Used in the Calculation (N)');
ylabel('Percentage Error (%)');
xticks(1:max_N_test);
set(gca, 'Color', 'w'); % Ensure the axes background is white
grid on;
