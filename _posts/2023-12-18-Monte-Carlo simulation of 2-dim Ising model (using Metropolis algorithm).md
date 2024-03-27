---
use_math: true
comments: true
title:  "Monte-Carlo simulation of 2-dim Ising model (using Metropolis algorithm)"
excerpt: "Numerical approache to the 2-dim Ising model" 
writer: Junyeop Kim
categories:
  - Computer Simulations
tags:
  - [Ising model]
  - [Monte-Carlo simulation]
  - [Fortran]
  - [Python]
date: 2023-12-18
last_modified_at: 2023-12-18
---
&nbsp;
&nbsp;
 
&ensp;요즘 하도 도서관에서 전공 공부만 하다보니 프로그래밍과 사이가 좀 많이 멀어진 것 같기도 하고, 때마침 휴학도 했겠다 시간이 좀 남아서 Fortran95과 Python으로 2-dim Ising model Monte-Carlo simulation 코드를 작성해봤다.

&ensp;사실 포트란은 전혀 쓸 줄 모르는 언어였는데 이번 기회에 한 번 공부해봤다. 아직은 많이 미숙해서 알고리즘(?)이 좀 더러워 보일 수도 있긴 한데 차차 나아지겠지 하핫... 

&nbsp;

<p style="text-align: center; font-size: 24px;">&bull;&ensp;&nbsp;&bull;&ensp;&nbsp;&bull;</p>

&nbsp;

### **1.  Evolutions of spin-configuration and magnetization w.r.t. iteration**
---

&nbsp;

&ensp;우선 iteration에 따라 spin configuration과 magnetisation이 어떻게 변하는지를 보여주는 프로그램을 만들어봤다.

&ensp;계산을 수행하고 데이터를 저장하는 부분인 main program은 Fortran95로 작성했고, visualization 부분은 python으로 작성했다. 아! magnetisation vs iteration graph는 그냥 GNUPLOT으로 만들었다.

&nbsp;

#### **Main Program (Fortran95)**
---

&nbsp;
언제나 그렇듯 PROGRAM ~ 으로 시작하자.

```fortran
PROGRAM ISING_MODEL
```

&nbsp;
   
&ensp;프로그램에 필요한 모든 변수들을 선언해주자. question mark가 있는 곳은 원하는대로 넣어주면 된다.

```fortran
  !---DECLARE VARIABLES---------------------------

    IMPLICIT NONE


    INTEGER(4) :: I_ROW, I_COL 
    INTEGER(4) :: SPIN_LOW, SPIN_COL
    INTEGER(4) :: ITR
    iNTEGER(4) :: PRE_MAGNETISATION

    INTEGER, PARAMETER :: DIM_ROW = ???, DIM_COL = ???
    INTEGER, PARAMETER :: NUMBER_TOTAL_SPIN = DIM_ROW * DIM_COL
    INTEGER, PARAMETER :: ITERATION = ???

    INTEGER, DIMENSION(DIM_ROW , DIM_COL) :: SPIN_CONFIG


    DOUBLE PRECISION, DIMENSION(ITERATION + 1) :: NORMALISED_MAGNETISATION

    DOUBLE PRECISION, PARAMETER :: J = ???                  ! SPIN CORRELATION
    DOUBLE PRECISION, PARAMETER :: GAMMA = 4.               ! NUMBER OF NEAREST LATTICE SITES (assume square lattice)
    DOUBLE PRECISION, PARAMETER :: BETA_C = 1/(J*GAMMA)     ! CRITICAL TEMPERATURE OF MEAN FIELD THEORY
    DOUBLE PRECISION, PARAMETER :: BETA_RATIO = ???         ! BETA_RATIO = BETA / BETA_C ... THEN BETA = BETA_C * BETA_RATIO

    DOUBLE PRECISION :: DEL_ENERGY, E_I, E_F
    DOUBLE PRECISION :: RND, RND_ROW, RND_COL


    !--- DIRECTORY RELATED VARIABLES
    
    CHARACTER(100) FOLDER_NAME

    INTEGER :: FU
    CHARACTER(100) FILE_NAME
    CHARACTER(100) FILE_ID
    
    INTEGER :: IERR, UNIT_NUM, IOSTAT


    !--- VARIABLES FOR THE PROGRAM EXECUATION TIME
    REAL :: START_TIME, END_TIME, TOT_TIME
```

   
   
   
필수는 아니지만, 프로그래밍 실행시간이 어느정도 나올지 궁금해서 한번 넣어봤다.

```fortran
!---LOAD CPU_TIME TO EVALUATE THE EXECUATION TIME---------------------------------
    
    CALL CPU_TIME(START_TIME)

!---------------------------------------------------
```

   
   
   
Initial spin configuration을 만들자.  
뭐 아무렇게나 만들어도 상관 없겠지만,  
        i)      completely random configuration (high temperature limit)  
        ii)     completely ordered(?) configuration (low temperature limit)  
이렇게 두 경우의 코드를 작성해봤다.

```fortran
 !---HIGH TEMPERATURE LIMIT ---------------------
    
    DO I_COL = 1, DIM_COL, +1

        DO I_ROW = 1, DIM_ROW, +1

            !---CHOOSE A REAL VALUE IN (0,1) RANGE
            CALL RANDOM_NUMBER(RND)

            !---COMPARE RND W/ 0.5
            !---IF RND < 0.5, GIVE UP-SPIN. ELSE, GIVE DOWN=SPIN
            IF ( RND < 0.50000000000000 ) THEN
                SPIN_CONFIG(I_ROW, I_COL) = -1
            ELSE   
                SPIN_CONFIG(I_ROW, I_COL) = +1
            END IF

        END DO
    
    END DO

    


!---LOW TEMPERATURE LIMIT

!    DO I_COL = 1, DIM_COL, +1
!        DO I_ROW = 1, DIM_ROW, +1
!            SPIN_CONFIG(I_ROW, I_COL) = +1
!        END DO
!    END DO
```

   
   
initial spin configuration의 (normalized) magnetisation을 계산하자.

```fortran
 !---CALCULATE THE MAGNETISATION OF INITIAL STATE-------------------------------
    
    ITR = 0

    PRE_MAGNETISATION = 0
    
    DO I_COL = 1, DIM_COL, +1
        
        DO I_ROW = 1, DIM_ROW, +1
        
            PRE_MAGNETISATION = PRE_MAGNETISATION + SPIN_CONFIG(I_ROW, I_COL)
        
        END DO
    
    END DO
    
    NORMALISED_MAGNETISATION(ITR) = 1. * PRE_MAGNETISATION / NUMBER_TOTAL_SPIN 
    !--- I PUT (1.*) TERM TO PREVENT FROME THE MAGNETISATION BECOMING INTEGER...!
```

   
   
   
사실 코드를 처음부터 python이나 julia로 작성했으면, spin configuration의 data를 바로 이미지로 변환해서 이미지 자체를 list에 차곡차곡 하나씩 쌓을 수 있기 때문에, 후술할 과정은 다른 언어라면 불필요한 과정일 수 있겠으나... (우리의 Fortran은 그런 packages 없기 때문에...)  
   
앞으로 DO loop를 돌리면서 얻게 될 each iteration step(?)에서의 spin configuration을 txt format으로 저장하려고 한다.  
이 spin configuration txt 파일들을 새로운 하위폴더를 만들어서 저장을 할 생각인데, 아래에 적어둔 code가 해당 역할을 수행한다.

```fortran
 !--- WRITE THE SPIN CONFIGURATION AS A TXT FILE, and MAGNETISATION DATA IN A NEW FOLDER

  ! Specify the folder name you want to create

    ! Write the integer into a string:
    FU = ITR + 20 !왜냐면 unit은 10부터 출발하자나...!!
    
    FOLDER_NAME = "spin_config"

  ! Use a system-specific command to create the folder
  ! Replace the following line with the appropriate command for your system (e.g., mkdir on Unix-like systems)
  ! On Windows, you can use "mkdir" as well.
    CALL SYSTEM("mkdir " // TRIM(FOLDER_NAME), IERR)

    IF (IERR == 0) THEN

    ! Specify the name of the text file to create inside the folder
        WRITE(FILE_ID, '(I0)') ITR
        FILE_NAME = TRIM(FOLDER_NAME) // "/config" // TRIM(ADJUSTL(FILE_ID)) // ".txt"
        
    ! Open the text file for writing
        OPEN( UNIT = FU , FILE = TRIM(FILE_NAME) , STATUS = "replace", ACTION = "write", IOSTAT = IOSTAT )

        IF (IOSTAT == 0) THEN
      ! Write data to the file
            WRITE(FU, *) SPIN_CONFIG
      ! Close the file
            CLOSE(FU)
        END IF

    END IF


    OPEN( 10, FILE = "magnetisation.txt", STATUS = "new" )    
    WRITE(10 ,*) ITR, NORMALISED_MAGNETISATION(ITR)
```

마지막 두 줄은 magnetisation을 기록하기 위한 새로운 txt file을 만들고, 파일을 열어서 데이터를 입력하도록 하는 코드이다. 이 파일은 그냥 main Fortran code와 동일한 directory에 저장할 생각이다.  
   
   
Do loop으로 iteration을 시작하자.

```fortran
 !---BEGIN ITERATION--------------------------------
    
    DO ITR = 1, ITERATION, +1
```

   
   
우선, 무작위로 spin element를 하나 뽑아서 뒤집어보자.

```fortran
    !---PICK A SPIN AT A RANDOM SITE---------------------
        CALL RANDOM_NUMBER(RND_ROW)
        CALL RANDOM_NUMBER(RND_COL)

        SPIN_ROW = 1 + FLOOR((DIM_ROW+1-1)*RND_ROW)
        SPIN_COL = 1 + FLOOR((DIM_COL+1-1)*RND_COL)

    !--- * FLIP THE CORRESPONDING PICKED SPIN TO OPPISITE DIRRECTION
        SPIN_CONFIG(SPIN_ROW, SPIN_COL) = (-1) * SPIN_CONFIG(SPIN_ROW, SPIN_COL)  
        !---[ (-1) FLIPS THE SPIN DIRRECTION ]
```

spin element의 위치를 matrix element의 것과 같은 형식으로 지정할 생각이다. (말이 조금 이상하긴 한데 (1,3)같이 위치를 나타내고 싶다는 뜻이다.)   
조심해야 할 부분이 있는데, RANDOM\_NUMBER( )로 가져온 float은 \[0,1) range에 있다. 그래서 \[1, DIM\_ROW or DIM\_COL\] range의 integer을 얻으려면, 위와같이 FLOOR function에 적절히 manipulation을 해주어야 한다.  
   
   
위에서 뽑은 spin element의 flipping 전후의 energy difference를 계산하자. 

```fortran
    !--- * CALCULATE THE ENERGY DIFFERENCE BEFORE AND AFTER THE SPIN FLIPPING -----------------
    
        IF ( SPIN_ROW == 1 .AND. SPIN_COL == 1 ) THEN
            
            DEL_ENERGY = (-2) * J * ( SPIN_CONFIG(SPIN_ROW+1, SPIN_COL) &
                                    + SPIN_CONFIG(SPIN_ROW, SPIN_COL+1) ) * SPIN_CONFIG(SPIN_ROW, SPIN_COL)

        ELSE IF ( SPIN_ROW == 1 .AND. SPIN_COL == DIM_COL ) THEN
            
            DEL_ENERGY = (-2) * J * ( SPIN_CONFIG(SPIN_ROW+1, SPIN_COL) &
                                    + SPIN_CONFIG(SPIN_ROW, SPIN_COL-1) ) * SPIN_CONFIG(SPIN_ROW, SPIN_COL) 
        
        ELSE IF ( SPIN_ROW == DIM_ROW .AND. SPIN_COL == 1 ) THEN

            DEL_ENERGY = (-2) * J * ( SPIN_CONFIG(SPIN_ROW-1, SPIN_COL) &
                                    + SPIN_CONFIG(SPIN_ROW, SPIN_COL+1) ) * SPIN_CONFIG(SPIN_ROW, SPIN_COL)

        ELSE IF ( SPIN_ROW == DIM_ROW .AND. SPIN_COL == DIM_COL ) THEN

            DEL_ENERGY = (-2) * J * ( SPIN_CONFIG(SPIN_ROW-1, SPIN_COL) &
                                    + SPIN_CONFIG(SPIN_ROW, SPIN_COL-1) ) * SPIN_CONFIG(SPIN_ROW, SPIN_COL)
        
        ELSE IF ( SPIN_COL == 1 ) THEN
            
            DEL_ENERGY = (-2) * J * ( SPIN_CONFIG(SPIN_ROW+1, SPIN_COL) + SPIN_CONFIG(SPIN_ROW-1, SPIN_COL) &
                                + SPIN_CONFIG(SPIN_ROW, SPIN_COL+1) ) * SPIN_CONFIG(SPIN_ROW, SPIN_COL)
        
        ELSE IF ( SPIN_COL == DIM_COL ) THEN

            DEL_ENERGY = (-2) * J * ( SPIN_CONFIG(SPIN_ROW+1, SPIN_COL) + SPIN_CONFIG(SPIN_ROW-1, SPIN_COL) &
                                + SPIN_CONFIG(SPIN_ROW, SPIN_COL-1) ) * SPIN_CONFIG(SPIN_ROW, SPIN_COL)
                                
        ELSE IF ( SPIN_ROW == 1 ) THEN

            DEL_ENERGY = (-2) * J * ( SPIN_CONFIG(SPIN_ROW+1, SPIN_COL) + SPIN_CONFIG(SPIN_ROW, SPIN_COL+1) &
                                + SPIN_CONFIG(SPIN_ROW, SPIN_COL-1) ) * SPIN_CONFIG(SPIN_ROW, SPIN_COL)
        
        ELSE IF ( SPIN_ROW == DIM_ROW ) THEN

            DEL_ENERGY = (-2) * J * ( SPIN_CONFIG(SPIN_ROW-1, SPIN_COL) + SPIN_CONFIG(SPIN_ROW, SPIN_COL+1) &
                                + SPIN_CONFIG(SPIN_ROW, SPIN_COL-1) ) * SPIN_CONFIG(SPIN_ROW, SPIN_COL)
        
        ELSE 
        
            DEL_ENERGY = (-2) * J * ( SPIN_CONFIG(SPIN_ROW+1, SPIN_COL) + SPIN_CONFIG(SPIN_ROW-1, SPIN_COL) &
                                + SPIN_CONFIG(SPIN_ROW, SPIN_COL+1) + SPIN_CONFIG(SPIN_ROW, SPIN_COL-1) ) & 
                                * SPIN_CONFIG(SPIN_ROW, SPIN_COL)

        END IF

!        (1,1)           ... (1,DIM_COL)
!        (2,1)           ... (2,DIM_COL)
!        .
!        .
!        .
!        (DIM_ROW,1)     ... (DIM_ROW,DIM_COL)
```

   
   
   

   
위에서 계산된 energy difference가 0보다 작으면 spin flipping을 accept하자.  
이건 뭐 당연하지... spin flipping 이후에 에너지가 더 낮아지는데 reject할 이유가 없잖아!  
   
근데, 만약 energy difference가 0보다 크다면, (0,1) range에서 random number 하나를 불러와서 exp(-beta\*del\_E)랑 비교를 할 건데,  
random number <  exp(-beta\*del\_E) 이면,  accept the spin flipping .  
random number >  exp(-beta\*del\_E) 이면,  reject the spin flipping .

```fortran
        IF ( DEL_ENERGY <= 0. ) THEN ! ACCEPT THE SPIN FLIP
            
            CONTINUE

        ELSE
            
            ! (DEL_ENERGY > 0)

            !--- CHOOSE A RANDOM NUMBER IN (0,1)
            CALL RANDOM_NUMBER(RND)
            
            IF ( RND < EXP(- BETA_C * BETA_RATIO * DEL_ENERGY) ) THEN ! ACCEPT THE SPIN FLIP
                
                CONTINUE

            ELSE ! REJECT THE SPIN FLIP
                
                SPIN_CONFIG(SPIN_ROW, SPIN_COL) = (-1) * SPIN_CONFIG(SPIN_ROW, SPIN_COL)
            
            END IF
        
        END IF
```

   
   
위의 IF statement가 끝나고 난 뒤의 최종 spin configuration과 normalized magnetisation을 txt file로 저장하자.

```fortran
    !--- WRITE AND SAVE DATA----------------------------

        !--- SPIN CONFIGURATION----------

        WRITE(FILE_ID, '(I0)') ITR

        FILE_NAME = TRIM(FOLDER_NAME) // "/config" // TRIM(ADJUSTL(FILE_ID)) // ".txt"
        
        ! Open the text file for writing
        OPEN( UNIT = FU , FILE = TRIM(FILE_NAME) , STATUS = "replace" , ACTION = "write" , IOSTAT = IOSTAT )

        IF (IOSTAT == 0) THEN
            ! Write data to the file
            WRITE(FU, *) SPIN_CONFIG
            ! Close the file
            CLOSE(FU)

        END IF

    
        !--- MAGNETISATION ----------------

        PRE_MAGNETISATION = 0
            
        DO I_COL = 1, DIM_COL, +1
            
            DO I_ROW = 1, DIM_ROW, +1
            
                PRE_MAGNETISATION = PRE_MAGNETISATION + SPIN_CONFIG(I_ROW, I_COL)
            
            END DO
            
        END DO
            
        NORMALISED_MAGNETISATION(ITR) = 1. * PRE_MAGNETISATION / NUMBER_TOTAL_SPIN


        WRITE(10 ,*) ITR, NORMALISED_MAGNETISATION(ITR)
```

   
   
DO LOOP을 닫고,

```fortran
!--- END ITERATION
    END DO
```

   
   
궁금하니까 프로그래밍 실행 총 소요시간도 한번 계산해보자.

```fortran
!---PROGRAM EXECUATION TIME-----------------------------------

    CALL CPU_TIME(END_TIME)

    TOT_TIME = END_TIME - START_TIME

    PRINT *, "IT TOOK ", TOT_TIME," SEC FOR THIS PROGRAM!"

!----------------------------------------------------------
```

   
   
이제 main Fortran program을 다 완성했다.

```fortran
 END PROGRAM ISING_MODEL
```

   
 다음으로, 위에서 만든 데이터들을 시각화하는 코드를 작성해보자.

---

#### **Visualization Using Python**

---

   
DO loop를 실행하며 계속 update되는 spin configuration을 시각화 하고 싶다.  
   
   
우선, 필요한 package들을 가져오자.

```python
import os
import numpy as np
from PIL import Image
import cv2
```

   
위에서 만든 spin configuration txt 파일들의 directory와 내가 만들 mp4 파일을 저장할 directory를 선언하자.

```python
# Define the input directory and file path
config_data = "C:\\Users\\f4jun\\OneDrive\\Desktop\\IsingModel_MCS\\spin_config"

# Specify the video file path (MP4 format)
video_directory = "C:\\Users\\f4jun\\OneDrive\\Desktop\\IsingModel_MCS"
video_file = os.path.join(video_directory, "IsingModel_wb.mp4")

# directory는 본인에게 맞게 적절히 바꿔서 넣어주면 된다.
```

   
   
각각의 spin configuration txt 파일들을 png 파일들로 변환한 후, 그 png 파일들을 모아서 list를 만들 생각이다.  
   
up spin (+1) elements는 검정색으로, down spin (-1) elements는 회색 내지 흰색으로 칠해보자.

```python
iteration = ?????

frames = []

for i in range(0, iteration + 1) :

    file_name = f"config{i}.txt"
    input_path = os.path.join(config_data, file_name)

    # Read the 1 x DIM_ROW*DIM_COL array from the text file
    flat_matrix = np.loadtxt(input_path, dtype = np.int32)

    # Reshape the flat matrix into a DIM_ROW x DIM_COL matrix
    matrix = flat_matrix.reshape( #DIM_ROW ??? , #DIM_COL ??? )

    # Create a grayscale image where 1 becomes black and -1 becomes gray
    grayscale_image = (matrix + 1) * 0.5 * 255  # 0 for black, 127.5 for gray

    # Convert the grayscale image to uint8 type
    grayscale_image = grayscale_image.astype(np.uint8)

    # Add to the image list
    frames.append(grayscale_image)
```

main fortran code의 iteration, DIM\_ROW, DIM\_COL 값들과 동일하게 넣어주면 된다.  
main code에서  SPIN\_ROW, SPIN\_COL 들을 INTEGER(4)로 declare 했으니까, np.loadtxt를 사용할 떄 data type은 integer 32로 지정해주면 된다.  
   
   
위에서 만든 이미지 list인 frames를 mp4 format으로 만들어주자.

```python
# Define the codec and frames per second (adjust as needed)
fourcc = cv2.VideoWriter_fourcc(*'mp4v')
fps = ???  # Frames per second

# Get the height and width of the frames
frame_height, frame_width = frames[0].shape

# Create a VideoWriter object to save the video
out = cv2.VideoWriter(video_file, fourcc, fps, (frame_width, frame_height), isColor=False)

# Write each frame to the video
for frame in frames:
    out.write(frame)

# Release the VideoWriter
out.release()
```

실행하고 나면 위에서 지정한 video\_directory에 mp4 file이 생성된다.  
   
 

---

   
  
몇 가지 상황에서의 실행 결과를 가져와봤다.  
  
    
 

**Completely Random Initial Spin Configuration  +  Low System Temperature (beta\_ratio = 1000.)**

---

<iframe src="https://play-tv.kakao.com/embed/player/cliplink/440849787?service=daum_tistory" width="600" height="600" frameborder="0" allowfullscreen="true"></iframe>

ITERATION = 1,000,000 // DIM\_ROW, DIM\_COL = 100 // fps = 100

위 영상은 iteration을 너무 많이 돌려서...  image list를 만들때 batch를 50정도 주고 만들었다.  
아무래도 dimension이 너무 커서 spontaneous magnetisation을 보려면 iteration을 훨씬 더 많이 줘야될 것 같다.

---

   
   
 

**Completely Random Initial State + Low System Temperature (beta\_ratio = 10000.)**

---

<iframe src="https://play-tv.kakao.com/embed/player/cliplink/440853245?service=daum_tistory" width="600" height="600" frameborder="0" allowfullscreen="true"></iframe>

ITERATION = 80,000 // DIM\_ROW, DIM\_COL = 20 // fps = 300

[##_Image|kage@bNchPx/btstk6dfq2c/02yx06gqUR6xdGkbo220sk/img.png|CDM|1.3|{"originWidth":745,"originHeight":475,"style":"alignCenter","width":600,"height":383,"caption":"위와 동일 ;&amp;amp;nbsp; spontaneous magnetisation이 잘 나타난다."}_##]

---

   
   
 

**Completely Random Initial Spin Configuration + High System Temperature (beta\_ratio = 0.01)**

---

<iframe src="https://play-tv.kakao.com/embed/player/cliplink/440850556?service=daum_tistory" width="600" height="600" frameborder="0" allowfullscreen="true"></iframe>

tITERATION = 50,000 // DIM\_ROW, DIM\_COL = 30 // fps = 500

[##_Image|kage@bkhkvO/btstk38Fz9A/Ei41VDKivTu5L9TkH7Nd7k/img.png|CDM|1.3|{"originWidth":640,"originHeight":475,"style":"alignCenter","width":600,"height":445,"caption":"위와 동일 ;&amp;amp;nbsp; magnetisation이 0 근처에서 계속 fluctuate 하는 것을 볼 수 있다."}_##]

---

   
   
 

**Well-Ordered Initial Spin Configuration + High System Temperature (beta\_ratio = 0.01)**

---

<iframe src="https://play-tv.kakao.com/embed/player/cliplink/440849763?service=daum_tistory" width="600" height="600" frameborder="0" allowfullscreen="true"></iframe>

ITERATION = 10000 // DIM\_ROW, DIM\_COL = 50 // fps = 100

[##_Image|kage@cCzpIu/btstljXEWpY/K9B8fW1qJtOUkd7KPMO0U0/img.png|CDM|1.3|{"originWidth":640,"originHeight":475,"style":"alignCenter","width":600,"height":445,"caption":"위와 동일 ; magnetisation이 0으로 converge한 후 지속적으로 fluctuate 하는 것을 볼 수 있다."}_##]

---

#### **2.   temperature     vs     magnetisation**

---

다음으로는 temperature의 변화에 따라 magnetisation이 어떻게 변하는지를 보여주는 program을 만들어봤다.

이것 또한 main program은 Fortran95, data plot은 python으로 작성했다.

#### **Main Program (Fortran95)**

---

```fortran
PROGRAM ISING_MODEL


    ! --- DECLARATION OF MAIN PROGRAM VARIABLES ---

    IMPLICIT NONE

    INTEGER(4) :: OUTER_ITERATION
    INTEGER, PARAMETER :: DATA_NUM = 10000

    
    !--- VARIABLES FOR ESTIMATING THE PROGRAM RUNNING TIME
    
    REAL :: START_TIME, END_TIME, TOT_TIME


!---RECORD PROGRAM RUNNING TIME---------------------------------
    
    CALL CPU_TIME(START_TIME)

!---------------------------------------------------



! --- START MAIN PROGRAM ---------------------------------------

    !--- CREATE A NEW FILE TO STORE MAGNETISATION DATA ------

    OPEN(10, FILE="mag.txt", STATUS="new")  


    !--- START DO LOOP --------------------------------------

    DO OUTER_ITERATION = 1, DATA_NUM, +10

        CALL MAIN(OUTER_ITERATION)
    
    END DO

    !--- END DO LOOP-----------------------------------------


    !--- CLOSE THE MAGNETISATION DATA FILE

    CLOSE(10)



!---PROGRAM RUNNING TIME-----------------------------------

    CALL CPU_TIME(END_TIME)

    TOT_TIME = END_TIME - START_TIME

    PRINT *, "IT TOOK ", TOT_TIME," SEC FOR THIS PROGRAM!"

!----------------------------------------------------------



CONTAINS

    SUBROUTINE MAIN(OUTER_ITERATION)

        ! --- DECLARATIO OF SUBROUTINE VARIABLES ---

        IMPLICIT NONE

        INTEGER(4), INTENT(IN) :: OUTER_ITERATION

        INTEGER(4) :: I_ROW, I_COL 
        INTEGER(4) :: SPIN_ROW, SPIN_COL
        INTEGER(4) :: ITR
        INTEGER(4) :: PRE_MAGNETISATION

        INTEGER, PARAMETER :: DIM_ROW = 20, DIM_COL = 20
        INTEGER, PARAMETER :: NUMBER_TOTAL_SPIN = DIM_ROW * DIM_COL
        INTEGER, PARAMETER :: ITERATION = 120000

        INTEGER, DIMENSION(DIM_ROW , DIM_COL) :: SPIN_CONFIG

        DOUBLE PRECISION, DIMENSION(ITERATION + 1) :: NORMALISED_MAGNETISATION

        DOUBLE PRECISION, PARAMETER :: J = 1.                   ! SPIN CORRELATION
        DOUBLE PRECISION, PARAMETER :: GAMMA = 4.               ! NUMBER OF NEAREST LATTICE SITES
        DOUBLE PRECISION, PARAMETER :: BETA_C = 1. / (J * GAMMA)     ! CRITICAL TEMPERATURE OF MEAN FIELD THEORY
        DOUBLE PRECISION :: BETA_RATIO

        DOUBLE PRECISION :: DEL_ENERGY, RND, RND_ROW, RND_COL

        BETA_RATIO = 1. * ((1. * OUTER_ITERATION) / 2500. )

        
        
!--- PREPARE AN INITIAL STATE ---

    !---HIGH TEMPERATURE LIMIT

        DO I_COL = 1, DIM_COL, +1
        
            DO I_ROW = 1, DIM_ROW, +1
        
                CALL RANDOM_NUMBER(RND)
        
                IF (RND < 0.500000000000000) THEN
                    SPIN_CONFIG(I_ROW, I_COL) = -1
                ELSE
                    SPIN_CONFIG(I_ROW, I_COL) = 1
                END IF
        
            END DO
        
        END DO



    !---LOW TEMPERATURE LIMIT

!        DO I_COL = 1, DIM_COL, +1
!            DO I_ROW = 1, DIM_ROW, +1
!                SPIN_CONFIG(I_ROW, I_COL) = 1
!            END DO
!        END DO



        !--- CALCULATE THE MAGNETISATION OF INITIAL STATE ---

        ITR = 0

        PRE_MAGNETISATION = 0

        DO I_COL = 1, DIM_COL, +1

            DO I_ROW = 1, DIM_ROW, +1

                PRE_MAGNETISATION = PRE_MAGNETISATION + SPIN_CONFIG(I_ROW, I_COL)

            END DO

        END DO

        NORMALISED_MAGNETISATION(ITR + 1) = 1. * PRE_MAGNETISATION / NUMBER_TOTAL_SPIN 



! --- BEGIN ITERATION ----------------------

        DO ITR = 1, ITERATION, +1


            ! --- PICK A SPIN AT RANDOM SITE ---

            CALL RANDOM_NUMBER(RND_ROW)
            CALL RANDOM_NUMBER(RND_COL)
            SPIN_ROW = 1 + FLOOR((DIM_ROW + 1 - 1) * RND_ROW)
            SPIN_COL = 1 + FLOOR((DIM_COL + 1 - 1) * RND_COL)
            

            ! --- FLIP THE CORRESPONDING PICKED SPIN TO OPPOSITE DIRECTION ---

            SPIN_CONFIG(SPIN_ROW, SPIN_COL) = -SPIN_CONFIG(SPIN_ROW, SPIN_COL)  
            

            ! --- CALCULATE THE ENERGY DIFFERENCE BEFORE AND AFTER THE SPIN FLIPPING ---

            IF ( SPIN_ROW == 1 .AND. SPIN_COL == 1 ) THEN
            
                DEL_ENERGY = (-2) * J * ( SPIN_CONFIG(SPIN_ROW+1, SPIN_COL) &
                                    + SPIN_CONFIG(SPIN_ROW, SPIN_COL+1) ) * SPIN_CONFIG(SPIN_ROW, SPIN_COL)

            ELSE IF ( SPIN_ROW == 1 .AND. SPIN_COL == DIM_COL ) THEN
            
                DEL_ENERGY = (-2) * J * ( SPIN_CONFIG(SPIN_ROW+1, SPIN_COL) &
                                    + SPIN_CONFIG(SPIN_ROW, SPIN_COL-1) ) * SPIN_CONFIG(SPIN_ROW, SPIN_COL) 
        
            ELSE IF ( SPIN_ROW == DIM_ROW .AND. SPIN_COL == 1 ) THEN

                DEL_ENERGY = (-2) * J * ( SPIN_CONFIG(SPIN_ROW-1, SPIN_COL) &
                                    + SPIN_CONFIG(SPIN_ROW, SPIN_COL+1) ) * SPIN_CONFIG(SPIN_ROW, SPIN_COL)

            ELSE IF ( SPIN_ROW == DIM_ROW .AND. SPIN_COL == DIM_COL ) THEN

                DEL_ENERGY = (-2) * J * ( SPIN_CONFIG(SPIN_ROW-1, SPIN_COL) &
                                    + SPIN_CONFIG(SPIN_ROW, SPIN_COL-1) ) * SPIN_CONFIG(SPIN_ROW, SPIN_COL)
        
            ELSE IF ( SPIN_COL == 1 ) THEN
            
                DEL_ENERGY = (-2) * J * ( SPIN_CONFIG(SPIN_ROW+1, SPIN_COL) + SPIN_CONFIG(SPIN_ROW-1, SPIN_COL) &
                                + SPIN_CONFIG(SPIN_ROW, SPIN_COL+1) ) * SPIN_CONFIG(SPIN_ROW, SPIN_COL)
        
            ELSE IF ( SPIN_COL == DIM_COL ) THEN

                DEL_ENERGY = (-2) * J * ( SPIN_CONFIG(SPIN_ROW+1, SPIN_COL) + SPIN_CONFIG(SPIN_ROW-1, SPIN_COL) &
                                + SPIN_CONFIG(SPIN_ROW, SPIN_COL-1) ) * SPIN_CONFIG(SPIN_ROW, SPIN_COL)
                                
            ELSE IF ( SPIN_ROW == 1 ) THEN

                DEL_ENERGY = (-2) * J * ( SPIN_CONFIG(SPIN_ROW+1, SPIN_COL) + SPIN_CONFIG(SPIN_ROW, SPIN_COL+1) &
                                + SPIN_CONFIG(SPIN_ROW, SPIN_COL-1) ) * SPIN_CONFIG(SPIN_ROW, SPIN_COL)
        
            ELSE IF ( SPIN_ROW == DIM_ROW ) THEN

                DEL_ENERGY = (-2) * J * ( SPIN_CONFIG(SPIN_ROW-1, SPIN_COL) + SPIN_CONFIG(SPIN_ROW, SPIN_COL+1) &
                                + SPIN_CONFIG(SPIN_ROW, SPIN_COL-1) ) * SPIN_CONFIG(SPIN_ROW, SPIN_COL)
        
            ELSE 
        
                DEL_ENERGY = (-2) * J * ( SPIN_CONFIG(SPIN_ROW+1, SPIN_COL) + SPIN_CONFIG(SPIN_ROW-1, SPIN_COL) &
                                + SPIN_CONFIG(SPIN_ROW, SPIN_COL+1) + SPIN_CONFIG(SPIN_ROW, SPIN_COL-1) ) & 
                                * SPIN_CONFIG(SPIN_ROW, SPIN_COL)

            END IF

!           (1,1)           ...    (1,DIM_COL)
!           (2,1)           ...    (2,DIM_COL)
!             .
!             .
!             .
!           (DIM_ROW,1)     ...    (DIM_ROW,DIM_COL)



!--- CALCULATE THE MAGNETISATION-------------------------
        
            IF ( DEL_ENERGY <= 0. ) THEN ! ACCEPT THE SPIN FLIP
                
                CONTINUE

            ELSE ! IF (DEL_ENERGY > 0)

                !--- CHOOSE A RANDOM NUMBER IN (0,1)
                CALL RANDOM_NUMBER(RND)
            
                IF ( RND < EXP(- BETA_C * BETA_RATIO * DEL_ENERGY) ) THEN ! ACCEPT THE SPIN FLIP
                
                    CONTINUE

                ELSE ! REJECT THE SPIN FLIP
                
                    SPIN_CONFIG(SPIN_ROW, SPIN_COL) = (-1) * SPIN_CONFIG(SPIN_ROW, SPIN_COL)

                END IF
        
            END IF


        
            PRE_MAGNETISATION = 0
            
            DO I_COL = 1, DIM_COL, +1

                DO I_ROW = 1, DIM_ROW, +1

                    PRE_MAGNETISATION = PRE_MAGNETISATION + SPIN_CONFIG(I_ROW, I_COL)

                END DO

            END DO
            
            NORMALISED_MAGNETISATION(ITR + 1) = 1. * PRE_MAGNETISATION / NUMBER_TOTAL_SPIN



        END DO
!--- END ITERATION-------------------------------------------------------



        ! --- WRITE TEMPERATURE AND MAGNETISATION ---
        
        WRITE(10, *) BETA_RATIO, NORMALISED_MAGNETISATION(ITERATION + 1)
    
    
    ! --- END SUBROUTINE MAIN ---
    
    END SUBROUTINE MAIN





! --- END PROGRAM ISING_MODEL ---

END PROGRAM ISING_MODEL
```

이번에는 SUBROUTINE을 사용해봤는데, 가장 바깥쪽에 OUTER\_ITERATION이 1부터 DATA\_NUM까지 가는 DO LOOP를 돌리고, 그 안에 계산을 수행하는 SUBROUTINE MAIN을 넣었다.   
 

BETA\_RATIO를 가장 바깥쪽 DO LOOP을 돌릴 때마다 변하게 만들고 싶어서 

BETA\_RATIO = 1. \* ((1. \* OUTER\_ITERATION) / 2500. )

요런 이상한 모양으로 만들어놨다.

BETA\_RATIO는 0부터 4까지의 범위이고, 이 사이를 10,000번 slice했다.

각각의 온도에서 iteration은 120,000번 돌렸다.

데이터 파일을 다음과 같이 12개를 만들자.

completely random initial spin configuration 파일 6개

well-ordered initial spin configuration 파일 6개 (all spins up 3개, all spins down 3개)

이제 이 txt 파일들을 파이썬으로 plot해보자!

---

#### **Plot data Using Python**

---

```python
import matplotlib.pyplot as plt
import numpy as np


### random initial spin configuration

highT_1_data = "C:\\Users\\f4jun\\OneDrive\\Desktop\\mag_h1.txt"
highT_1 = np.loadtxt(highT_1_data)
x_h1 = highT_1[:,0]
y_h1 = highT_1[:,1]

highT_2_data = "C:\\Users\\f4jun\\OneDrive\\Desktop\\mag_h2.txt"
highT_2 = np.loadtxt(highT_2_data)
x_h2 = highT_2[:,0]
y_h2 = highT_2[:,1]

highT_3_data = "C:\\Users\\f4jun\\OneDrive\\Desktop\\mag_h3.txt"
highT_3 = np.loadtxt(highT_3_data)
x_h3 = highT_3[:,0]
y_h3 = highT_3[:,1]

highT_4_data = "C:\\Users\\f4jun\\OneDrive\\Desktop\\mag_h4.txt"
highT_4 = np.loadtxt(highT_4_data)
x_h4 = highT_4[:,0]
y_h4 = highT_4[:,1]

highT_5_data = "C:\\Users\\f4jun\\OneDrive\\Desktop\\mag_h5.txt"
highT_5 = np.loadtxt(highT_5_data)
x_h5 = highT_5[:,0]
y_h5 = highT_5[:,1]

highT_6_data = "C:\\Users\\f4jun\\OneDrive\\Desktop\\mag_h6.txt"
highT_6 = np.loadtxt(highT_6_data)
x_h6 = highT_6[:,0]
y_h6 = highT_6[:,1]



### well-ordered initial spin configuration , all spins up

lowT_u1_data = "C:\\Users\\f4jun\\OneDrive\\Desktop\\mag_lu1.txt"
lowT_u1 = np.loadtxt(lowT_u1_data)
x_lu1 = lowT_u1[:,0]
y_lu1 = lowT_u1[:,1]

lowT_u2_data = "C:\\Users\\f4jun\\OneDrive\\Desktop\\mag_lu2.txt"
lowT_u2 = np.loadtxt(lowT_u2_data)
x_lu2 = lowT_u2[:,0]
y_lu2 = lowT_u2[:,1]

lowT_u3_data = "C:\\Users\\f4jun\\OneDrive\\Desktop\\mag_lu3.txt"
lowT_u3 = np.loadtxt(lowT_u3_data)
x_lu3 = lowT_u3[:,0]
y_lu3 = lowT_u3[:,1]


### well-ordered initial spin configuration , all spins down

lowT_d1_data = "C:\\Users\\f4jun\\OneDrive\\Desktop\\mag_ld1.txt"
lowT_d1 = np.loadtxt(lowT_d1_data)
x_ld1 = lowT_d1[:,0]
y_ld1 = lowT_d1[:,1]

lowT_d2_data = "C:\\Users\\f4jun\\OneDrive\\Desktop\\mag_ld2.txt"
lowT_d2 = np.loadtxt(lowT_d2_data)
x_ld2 = lowT_d2[:,0]
y_ld2 = lowT_d2[:,1]

lowT_d3_data = "C:\\Users\\f4jun\\OneDrive\\Desktop\\mag_ld3.txt"
lowT_d3 = np.loadtxt(lowT_d3_data)
x_ld3 = lowT_d3[:,0]
y_ld3 = lowT_d3[:,1]



# Graph setting
plt.figure(figsize=(12, 8))

plt.plot(x_h1, y_h1, marker='x', markersize=2, linestyle='', color='r', label='completely ramdom initial spin configuration')
plt.plot(x_h2, y_h2, marker='x', markersize=2, linestyle='', color='r')
plt.plot(x_h3, y_h3, marker='x', markersize=2, linestyle='', color='r')
plt.plot(x_h4, y_h4, marker='x', markersize=2, linestyle='', color='r')
plt.plot(x_h5, y_h5, marker='x', markersize=2, linestyle='', color='r')
plt.plot(x_h6, y_h6, marker='x', markersize=2, linestyle='', color='r')

plt.plot(x_lu1, y_lu1, marker='x', markersize=2, linestyle='', color='b', label='well-ordered initial spin configuration (all spins up)')
plt.plot(x_lu2, y_lu2, marker='x', markersize=2, linestyle='', color='b')
plt.plot(x_lu3, y_lu3, marker='x', markersize=2, linestyle='', color='b')

plt.plot(x_ld1, y_ld1, marker='x', markersize=2, linestyle='', color='g', label='well-ordered initial spin configuration (all spins down)')
plt.plot(x_ld2, y_ld2, marker='x', markersize=2, linestyle='', color='g')
plt.plot(x_ld3, y_ld3, marker='x', markersize=2, linestyle='', color='g')


plt.xlabel('Beta  /  Beta _ MFT critical (= beta * [ J * gamma ] )', fontsize = 12 )
plt.ylabel('Normalized Magnetization', fontsize = 12 )
plt.title('2-dim Ising Model Monte-Carlo Simulation', fontsize = 15, pad = 20)
plt.legend()
plt.grid(True)

plt.show()
```

코드를 실행하면 다음과 같은 그래프를 얻는다.

---

[##_Image|kage@cNoqlX/btstw4AdPYt/oZJykCNCnIChD6ToKjvIx0/img.png|CDM|1.3|{"originWidth":1069,"originHeight":762,"style":"alignCenter","filename":"edited_output.png"}_##]

만족스러운 결과이군...


---
