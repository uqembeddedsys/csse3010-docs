# MYLIB Guide

# Introduction
The MyLib is a library folder that contains .c and .h files which you will develop for the external peripherals and commonly used library functions that you will use. External peripherals are devices that are not part of the microcontroller unit, i.e. LED Light-Bar or Joystick. Each time you use a peripheral you will create an associated MyLib file that contains the Application Interface (API) functions for that particular peripheral. Commonly used library functions are purely software based features, e.g. Hamming or CRC libraries.

As you develop further code, you will continue to update the MyLib files by adding new functionalities required by the stages and projects. Mylib files should be developed in a way that will allow you to reuse your previously developed code for later stages and projects, without having to copy and paste peripheral code.


# Folder Structure

To ensure all course materials and your own work are well organised, we require that you implement the folder hierarchy and naming conventions displayed in the figure below.

\hrule
\begin{flushleft}
	\begin{forest}
	for tree={
		font=\ttfamily,
		grow'=0,
		folder,
		if n children=0{
			before typesetting nodes={
				tempdima=\iconsepfrompath+\iconsep+8*\touchsize,
				content/.wrap value={\expandafter\hskip \foresteregister{tempdima}#1},
			},
			tikz={%
				\pic [xshift=\iconsepfrompath] at (.west) {mkdir};
			},
		}{
			if level=0{
				tikz={%
					\pic [xshift=\iconsepfrompath] at (.west) {mkdir};
				},
				before typesetting nodes={
					tempdima=\iconsep+12*\mkdirsize,
					content/.wrap value={\expandafter\hskip \foresteregister{tempdima}#1},
				},
			}{
				tikz={%
					\pic [xshift=\iconsepfrompath] at (.west) {mkdir};
				},
				before typesetting nodes={
					tempdima=\iconsepfrompath+\iconsep+12*\mkdirsize,
					content/.wrap value={\expandafter\hskip \foresteregister{tempdima}#1},
				},
			},
		},
	},
	[\$HOME
	[csse3010
	[sourcelib]
	[mylib
	[lta1000g]
	[joystick]
	]
	[project]
	[stages
	[stage1
	]
	[stage2]
	]
	]
	]
\end{forest}
\end{flushleft}
\hrule
~
		  
First you will create a \textbf{csse3010} folder under your home directory. This folder serves as your git group folder. Here, you must add the sourcelib, mylib, project and stage git repositories. You will need to clone the \textbf{\textbf{sourcelib}} repository, which contains the examples, HAL and OS library files.

You will have to create the \textbf{mylib}, \textbf{project} and \textbf{stage} git repositories. These  will contain all of your work. The \textbf{mylib} repository will contain all your mylib files. Each mylib driver will have its own folder, e.g. \textbf{joystick}. The \textbf{stage} repository will also contain a folder for each stage (named \textbf{stage1}, \textbf{stage2} etc.).

# Mylib Files and Folder Organisation

## {Mylib folder and files
The mylib folder should contain source (.c) and header (.h) files, which are specific to a function or peripheral. Examples are seen in Table 1. There are 4 types of source (.c) and header (.h) files that you will use.

\begin{itemize}
	\item Hardware Abstract Layer (\textbf{HAL}) – contains low level hardware accessing functions.
		\subitem - sxxxxxx\_hal\_peripheral.c/.h
	\item Operating System (\textbf{OS}) – contains OS specific functions (e.g. using the FreeRTOS functions)
		\subitem - sxxxxxx\_os\_peripheral.c/.h
	\item Command Line Interface (\textbf{CLI}) – contains CLI functions (e.g. using the FreeRTOS CLI library functions)
		\subitem - o	sxxxxxx\_cli\_peripheral.c/.h
	\item Library Function (\textbf{LIB}) – contains commonly used functions that are not HAL, OS or CLI related functions.
\end{itemize}

For guidelines for the OS and CLI mylib files, see the csse3010\_mylib\_os\_peripheral\_guide.pdf on Blackboard.

\begin{table}[H]
	\centering   
	\caption{Example Files}
	\renewcommand{\arraystretch}{1}
	\begin{tabular}{|p{5cm}|p{5cm}|}		
		\hline
		\textbf{Peripheral} & \textbf{File name} \\ \hline
		LED Light Bar HAL & sxxxxxx\_hal\_lightbar.c \\ \hline
		Joystick OS & sxxxxxx\_os\_joystick.c \\ \hline
		Pan Tilt CLI & sxxxxxx\_cli\_pantilt.c \\ \hline	
		Hamming encoder/decoder & sxxxxxx\_lib\_hamming.c \\ \hline	
	\end{tabular}
	%}
\end{table}

## Mylib HAL File Structure
A mylib HAL .c file for a particular peripheral contains external functions to initialise, utilise (get or set) and control that peripheral. Internal functions can also be present in mylib .c files. External and internal functions and their naming convention are elaborated on below in section \ref{ref:convention}. Each mylib .c file must contain an \texttt{init()} function and a \texttt{deinit()} function, which contain the initialisation an de-initialisation code for that particular peripheral.

## Mylib LIB File Structure
A mylib LIB .c file contains external functions for commonly used features. There are no required functions. Internal functions can also be present in these filess.

# Mylib File and Header Description Section

Each mylib source file (.c) must contain a top comment section at the beginning of the file that states the purpose of the file the external functions defined within. An example is given below. The mylib header file (.h) should also contain the descriptive section and list of external functions. \\

```
/**   
 ***************************************************************
 * @file    mylib/ledbar/sxxxxxx_hal_ledbar.c    
 * @author  MyName - MyStudent ID   
 * @date    22022018   
 * @brief   MY peripheral driver   
 *	     REFERENCE: DON'T JUST COPY THIS BLINDLY.pdf   
 ***************************************************************
 *     EXTERNAL FUNCTIONS
 ***************************************************************
 * sxxxxxx_hal_my_init() - intialise LED bar
 * sxxxxxx_hal_my_set() - set LED bar value
 ***************************************************************
 */
```

# Mylib Naming Conventions

Naming conventions for mylib files and external and internal functions.

## File Naming Convention

Files must contain your student login (sxxxxxx) and the name of the peripheral. The name must be lower case. For example: `sxxxxxx_hal_peripheral.c`

## External Function Naming Convention

 External functions are called outside the .c file in which they are defined. External functions must contain your student login (sxxxxxx), the HAL/OS/CLI/LIB prefix, the name of the file and the purpose of the function. The name must be lower case. External functions should be declared in the corresponding header (.h) file with the \textbf{extern} descriptor (template below).

 \hfill \break
\textbf{extern \textcolor{green}{sxxxxxx}\_hal\_\textcolor{blue}{peripheral}\_function()} \\

For example: The function for getting the joystick x value (returns an unsigned short) defined in \texttt{s123456\_hal\_joystick.c} should be named \\

`extern unsigned short s123456_hal_joystick_getx()`

Table 2 contains naming suggestions for external functions commonly found in a mylib HAL file. 
\begin{table}[H]
	\centering   
	\caption{HAL Peripheral Driver External Functions}
	\renewcommand{\arraystretch}{1}
	\begin{tabular}{|p{3cm}|p{8cm}|}		
		\hline
		\textbf{Function Name} & \textbf{Purpose} \\ \hline
		\texttt{\_init()} & Initialise and configure peripheral (i.e. set GPIO pins, ADC parameters, etc.) \\ \hline
		\texttt{\_read()} & Read value(s) \\ \hline
		\texttt{\_write()} & Write value(s) \\ \hline	
		\texttt{\_ctrl()} & Change configuration parameters (different to \texttt{init()}) \\ \hline	
		\texttt{\_deinit()} & De-initialise the peripheral (i.e. disable peripheral interrupts and shut down peripheral) \\ \hline	
	\end{tabular}
	%}
\end{table}

## Internal Function Naming Convention
Internal functions are only called within the file in which they are defined. Internal functions should only contain the name of the peripheral file and the purpose of the function. The name must be lower case (template below). \\

\textbf{\textcolor{blue}{peripheral}\_function()} \\

For example: The function for converting joystick ADC value to voltage (returns an unsigned short) located in \texttt{s123456\_joystick.c} should be named\\

`unsigned short joystick_adc2voltage(unsigned short raw_adc)`


## Header File
Header (.h) files should have the same name as the .c file. Header files need to begin with a \textbf{\#ifdef} statement and end with \textbf{\#endif}, to prevent re-entrancy errors. \\

```
#ifndef SXXXXXX_HAL_HEADERNAME_H
#define SXXXXXX_HAL_HEADERNAME_H

/* Header file code */

#endif
```
