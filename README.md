# a-rose-script--demo
#### outputs time in sexigesimal-binary representation
- this is how we see our clock faces on Gethen
![demo script's output](https://user-images.githubusercontent.com/98284211/172931510-2ed1fa73-2949-4854-81e0-133784b6419a.png "rose script second59")

>```
>#a rose script (demo-version) outputs time in sexigesimal-binary representation
>#    Copyright (C) 2014-2022  irulanCorrino
>#
>#    This program is free software: you can redistribute it and/or modify
>#    it under the terms of the GNU General Public License as published by
>#    the Free Software Foundation, either version 3 of the License, or
>#    (at your option) any later version.
>#
>#    This program is distributed in the hope that it will be useful,
>#    but WITHOUT ANY WARRANTY; without even the implied warranty of
>#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
>#    GNU General Public License for more details.
>#
>#    You should have received a copy of the GNU General Public License
>#    along with this program.  If not, see <https://www.gnu.org/licenses/>.
>#____________________________________________________________________________
>#
>#  _time_(sexigesimal-binary_representation)__________|*a remark written in 2022_____
># __________it is a cleaned version of original [non-realtime] script but i have lost
># ____my memory since then so i cannot recollect what were all those comments about
># __________________________________________end of the  remark written in 2022*|_____
># circle
>learn circle {
>  for $n = 1 to 180 {
>    turnleft 2
>    forward 0.6
>    }
> }
>#_test_version |*[mocking a call to system time function]*|
>$agreement = true
>#
>while $agreement {
>$time = -1
>while ($time < 59) {
>$time = $time + 1
>#
>if not $time { $fork = 0 }
>#
>#_end_of_test_codesection_ |*probably this comment was imported and forgotten here*|
>reset
>spritehide
>#_logic
>#$time = 0
>$exception = false
>$oddity = false
>#_--actually a null is even
>#$time = ask "+ time (less then fifty nine or equal to) +"
>if (mod $time, 2) { $oddity = true }
># stem --'repeats_twice'
>$petal = 0
>if ($time > 1) {
>   if ($time > 15) {
>      $sector = mod $time, 15
>      $petal = ( $time - $sector ) / 15
>      if not $sector {
>         $petal = $petal - 1
>         if (mod $petal, 2) { $oddity = not $oddity }
>         $fork = 7
>       }
>       else {
>         if (mod $petal, 2) { $oddity = not $oddity }
>         if ($sector == 1) {
>          $exception = true
>          $fork = 0
>          }
>          else {   
>            if (not mod $sector, 2) { $fork = $sector / 2 }
>             else { $fork = ( $sector - 1 ) / 2 }
>            }
>       }
>    }
>    else {
>      if not $oddity { $fork = $time / 2 }
>       else { $fork = ( $time - 1 ) / 2 }
>      }
> }
># minutes _'$fork {'(or anything else at a base of sixty) --evenness
>#learn triad
>#
>#
>##learn corolla
># actually roses are with five petals _'$petal, $fork {'
>#
>#_this_commentars_were_the_parts_of_non-script_program
>#____________________|*then i meant non-realtime script*|
>#_interface
>canvassize 200, 200
>go 100, 100
>if $time { spritehide }
>print $time
>turnleft 315
>turnleft 90 * $petal
>if not $exception {
>    turnright 30
>    while ($fork > 0) {
>     $bit = false
>     $remainder = mod $fork, 2
>     penup
>     forward 20
>     if $remainder {
>      pendown
>      $bit = true
>      }
>     forward 70
>     $fork = ($fork - $remainder) / 2 
>     if $bit { penup }
>     forward 20
>     turnleft 120
>     }
> }
> else {
>  turnright 30
>  repeat 3 {
>     turnleft 120
>     $fork = 7
>     turnright 30
>     while ($fork > 0) {
>      $bit = false
>      $remainder = mod $fork, 2
>      penup
>      forward 20
>      if $remainder {
>       pendown
>       $bit = true
>       }
>      forward 70
>      $fork = ($fork - $remainder) / 2 
>      if $bit { penup }
>      forward 20
>      turnleft 120
>      }
>    }
> }
>go 100, 100
># i think it resembles ovaries
># gynoecium _
>if $oddity {
>#_an_explanation_(uncomment_it)_ _
># pendown
> forward 54 / 3.1416
> turnleft 90
> pendown
> circle
> }
>#_repeating_branch_}_(test)_
>if not $time { wait 0.7 }
>if ( not $oddity ) and ( not $exception ) { wait 0.5 }
>if $exception { wait 0.2 }
>}
>#_'_weaver_answer_to_me_'_branch_}_(test)_
>$answer = 1
>$answer = ask "_ * shall i repeat digits drawing * (true or false) _"
>if not $answer { $agreement = false }
>}
>spriteshow
>```
