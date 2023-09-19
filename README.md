# Euler-Pi-High-Precision-in-C-with-libraries-MPC-MPFR-GMP
ian@ian-HP-Convertible-x360-11-ab1XX:~$ gcc EulerPi.c  -lmpc -lmpfr -lgmp -o EulerPi 
ian@ian-HP-Convertible-x360-11-ab1XX:~$ ./EulerPi
Computed value of e^(i*pi/4) is (7.071067811865475244008443621048490392848359376884740365883398689953662392310509e-1 7.071067811865475244008443621048490392848359376884740365883398689953662392310509e-1)
pi = 3.141592653589793238462643383279502884197169399375105820974944592307816406286199e0
ian@ian-HP-Convertible-x360-11-ab1XX:~$ cat EulerPi.c
#include <stdio.h>
#include <mpc.h>
#include <mpfr.h>

#define PREC 256

int main()
{
	mpc_t rx;
	mpc_t ipi4;
	mpfr_t pi;

	mpfr_set_default_prec(PREC);
	mpc_init2(rx, PREC);
	mpc_init2(ipi4, PREC);
	mpfr_init(pi);
	mpfr_const_pi(pi, MPFR_RNDD);
	mpc_set_fr(ipi4, pi, MPC_RNDDD);
	mpc_mul_i(ipi4, ipi4, 1, MPC_RNDDD);
	mpc_div_ui(ipi4, ipi4, 4, MPC_RNDDD);
	mpc_exp(rx, ipi4, MPC_RNDDD);

	printf("Computed value of e^(i*pi/4) is ");
	mpc_out_str(stdout, 10, 0, rx, MPC_RNDDD);
	printf("\n%s","pi = ");
	
	mpfr_out_str(stdout, 10, 0, pi, MPC_RNDDD);
	
	printf("\n");
	return 0;
}
ian@ian-HP-Convertible-x360-11-ab1XX:~$ sloccount EulerPi.c
Have a non-directory at the top, so creating directory top_dir
Adding /home/ian/EulerPi.c to top_dir
Categorizing files.
Finding a working MD5 command....
Found a working MD5 command.
Computing results.


SLOC	Directory	SLOC-by-Language (Sorted)
25      top_dir         ansic=25


Totals grouped by language (dominant language first):
ansic:           25 (100.00%)




Total Physical Source Lines of Code (SLOC)                = 25
Development Effort Estimate, Person-Years (Person-Months) = 0.00 (0.05)
 (Basic COCOMO model, Person-Months = 2.4 * (KSLOC**1.05))
Schedule Estimate, Years (Months)                         = 0.07 (0.80)
 (Basic COCOMO model, Months = 2.5 * (person-months**0.38))
Estimated Average Number of Developers (Effort/Schedule)  = 0.06
Total Estimated Cost to Develop                           = $ 562
 (average salary = $56,286/year, overhead = 2.40).
SLOCCount, Copyright (C) 2001-2004 David A. Wheeler
SLOCCount is Open Source Software/Free Software, licensed under the GNU GPL.
SLOCCount comes with ABSOLUTELY NO WARRANTY, and you are welcome to
redistribute it under certain conditions as specified by the GNU GPL license;
see the documentation for details.
Please credit this data as "generated using David A. Wheeler's 'SLOCCount'."
ian@ian-HP-Convertible-x360-11-ab1XX:~$ 

