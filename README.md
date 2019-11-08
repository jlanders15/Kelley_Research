# Mitochondrial Chromosome Comparison Analysis in Population VCF files 
Log book for mitochondrial chromosome comparison in population vcd files using bedtools. All code was run on WSU high performance computer



# Populations tested
Banos, Bonita, Esperanza, Gloria, Ixta, Lluvia, Pso, Rosita, Vg, Vs

/data/kelley/projects/pmex/capture/anthony_analysis/population_vcf_files/

	banos_combined.vcf.gz
	bonita_combined.vcf.gz
	esperanza_combined.vcf.gz
	gloria_combined.vcf.gz
	ixta_combined.vcf.gz
	lluvia_combined.vcf.gz
	pso_combined.vcf.gz
	rosita_combined.vcf.gz
	vg_combined.vcf.gz
	vs_combined.vcf.gz

## Trim VCF Files
Trimming the vcf files to only include mitochondrial DNA using VCF Tools


/anthony_analysis/vcf_scripts_jl/onlyMito/onlyMito.populations.VCF.srun

	#!/bin/bash
	#SBATCH --partition=kamiak
	#SBATCH --job-name=jake.populationVCF.mitoONLY		### job name
	#SBATCH --output=popVCF.onlyMito_%A_%a.out 		### output name
	#SBATCH --error=popVCF.onlyMito_%A_%a.err 		### error name
	#SBATCH --mail-type=ALL
	#SBATCH --mail-user=jake.landers@wsu.edu 	### email address for notifications
	#SBATCH --time=7-00:00:00
	#SBATCH --nodes=1
	#SBATCH --ntasks-per-node=1
	#SBATCH --ntasks=1
	#SBATCH --cpus-per-task=1
	#SBATCH --array=1-10:1	### lines that the array will use
	#SBATCH --mem=26000		### ammount of ram used by program (in mB)

	sample_name=$(sed -n ''$SLURM_ARRAY_TASK_ID'p' pop.vcf.datasheet.txt | awk '{print$1}')
	file_name=$(sed -n ''$SLURM_ARRAY_TASK_ID'p' pop.vcf.datasheet.txt | awk '{print$2}')

	cd /data/kelley/projects/pmex/capture/anthony_analysis/population_vcf_files/

	vcftools --gzvcf $file_name --chr KC992998.1 --out ../filtered_vcff/onlyMito_popVCF/$sample_name.popVCF.onlyMito.output


Script reads off of the following text file:

/anthony_analysis/vcf_scripts_jl/onlyMito/pop.vcf.datasheet.txt/

	BEN banos_combined.vcf.gz 
	BON bonita_combined.vcf.gz 
	ESP esperanza_combined.vcf.gz 
	GLO gloria_combined.vcf.gz 
	IXT ixta_combined.vcf.gz 
	LUV lluvia_combined.vcf.gz 
	PSO pso_combined.vcf.gz 
	ROS rosita_combined.vcf.gz 
	VG vg_combined.vcf.gz 
	VS vs_combined.vcf.gz 



