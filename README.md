%% SISTEMA INTELIGENTE DE GESTION ENERGETICA (SIGE)
% Simulacion de la generacion y demanda electrica durante 24 horas 

clc;
clear;
close all;

%% 1. Vector de tiempo
% Cada posicion representa una hora del dia
horas = 1:24;

%% 2. Generacion solar (kW)
% La produccion es cero durante la noche
% La potencia maxima es de 25 kW en la hora 12.

P_solar = [ ...            % Horas 1 a 5
    0 0 0 0 0 ...          % Horas 6 a 12
    3 8 14 19 22 24 25 ... % Horas 13 a 18
    24 21 17 12 6 2 ...    % Horas 19 a 24
    0 0 0 0 0 0];

%% 3. Generacion eolica (kW)
% Valores variables que simulan los cambios del viento.
% La potencia no supera el limite nominal de 15 kW.

P_eolica = [ ...
    7 9 6 8 5 10 12 9 ...
    11 8 13 10 7 12 14 9 ...
    11 8 6 10 13 7 5 9];

%% 4. Generacion hibrida total (kW)
% Suma de la generacion solar y eolica hora por hora.

P_total = P_solar + P_eolica;

%% 5. Demanda electrica de la comunidad (kW)
% Horas 1 a 5 y 22 a 24: consumo base de 2 a 4 kW.
% Horas 6 a 17: consumo diurno de 6 a 10 kW.
% Horas 18 a 21: demanda maxima de 15 kW.

P_demanda = [ ...
    3 2 3 4 3 ...                 % Horas 1 a 5
    6 7 8 9 8 10 9 8 7 9 10 8 ... % Horas 6 a 17
    15 15 15 15 ...               % Horas 18 a 21
    4 3 2];                       % Horas 22 a 24

%% 6. Grafica de generacion total y demanda

figure;

plot(horas, P_total, '-ob', 'LineWidth', 1.8);
hold on;
plot(horas, P_demanda, '-sr', 'LineWidth', 1.8);

title('SIGE: Generacion Total vs Demanda Electrica');
xlabel('Tiempo en horas');
ylabel('Potencia en kilovatios (kW)');

legend('Generacion Total', 'Demanda de la Comunidad', ...
       'Location', 'best');

grid on;
xlim([1 24]);
xticks(1:24);

hold off;

%% 7. Mostrar resultados en la ventana de comandos

disp('Hora | Solar | Eolica | Generacion Total | Demanda');
disp([horas' P_solar' P_eolica' P_total' P_demanda']);
