#################

tcga_query documentation

author: Nolan Kuza (nkuza8@gmail.com)
date:	1-17-19

#################

Parse vcf files by deleting metadata and keeping only selected columns.

usage: tcga_query.py [-h] -i INPUT -t {mRNA,miRNA,both} [-q] [-m MANIFEST] [-d METADATA]

required arguments:
  -i INPUT, --input INPUT
                        The name of the input file containing a list of TCGA ids. Each
						id can be quoted or unquoted. Only the first 12
						characters of each id will be used.
  -t {mRNA,miRNA,both}, --type {mRNA,miRNA,both}
						Type of data to export. Option 'both' specifies both mRNA AND miRNA.

optional arguments:
  -h, --help            show the help message and exit
  -q, --query           If this option is included, a TCGA QUERY will be
						outputed to stdout and a manifest will not be
						downloaded.
  -m MANIFEST, --manifest MANIFEST
                        The name of the file to download the manifest to (will
                        overwrite file if it already exists). If this argument
						is not specified (and neither is -q), manifest will be
                        outputed to stdout.
  -d METADATA, --metadata METADATA
                        The name of the file to download the JSON metadata to (will
                        overwrite file if it already exists). If this argument
						is not specified (and neither is -q), metadata will be
                        outputed to stdout.

example:

	We want to query mRNA with TCGA id in input.txt and then download the manifest to mani.txt and the metadata to meta.json.

	input.txt:
		TCGA-05-4250
		"TCGA-05-4405"
		TCGA-05-4415-0192
		"TCGA-05-4417-0164"
	
	Then run with:
		python tcga_query.py -i input.txt -t miRNA -m mani.txt -d meta.json
		
	The program will write the following into mani.txt:
		id	filename	md5	size	state
		10b6df33-8f32-4ed9-b1b1-8867be485a2f	6e98ba8f-e00d-470c-832f-adc3dc6956a6.FPKM.txt.gz	61e93edfed714da7280bba70c08d0f41	505452	released
		a07c86e4-b157-49f7-b541-7e1c0b3cf27b	4ed68c20-e7f2-4b40-97f1-4f8a3ddae0a9.FPKM.txt.gz	895c980876df6ecde9fdb681edec209e	514950	released
		46ea8adf-e1bd-4e3b-8cea-307ca36073d0	6e98ba8f-e00d-470c-832f-adc3dc6956a6.FPKM-UQ.txt.gz	7ca897843589d989fcd429af53b3cad0	505835	released
		3653dfea-049c-4ae8-8aca-cf6799797dd7	dc76cdde-f77f-4604-94c4-0b150b9a56b4.htseq.counts.gz	71bcd107585e69b96e909076cc9c1b61	249745	released
		156acd96-fb20-4083-ace0-db465133670c	d011c9fc-3598-4f0b-b059-85d63de31a9f.FPKM.txt.gz	5970f4595f6d210bfd1f9b65b045a972	501941	released
		0f5f287b-ee07-47b1-9d71-03cacffbdc21	dc76cdde-f77f-4604-94c4-0b150b9a56b4.FPKM-UQ.txt.gz	03d16f7df1a9a79f7b764bb2e5ee0005	512590	released
		545b3be7-9189-4e1e-85d6-af4a7540ec97	4ed68c20-e7f2-4b40-97f1-4f8a3ddae0a9.htseq.counts.gz	2098e89ef4ad8b42d27bd05b38d933b4	253840	released
		3471e070-167d-4af2-b9c6-38fbd4e86add	4ed68c20-e7f2-4b40-97f1-4f8a3ddae0a9.FPKM-UQ.txt.gz	cac01aaa0b0c89bfcb765b9cf606f26c	516514	released
		9c740043-d02a-412a-851b-cfcb625e04c4	6e98ba8f-e00d-470c-832f-adc3dc6956a6.htseq.counts.gz	74b0373a0ccc28097775e4557fedfb00	249824	released
		1fae764e-3807-4565-a78d-5ea852d327a7	d011c9fc-3598-4f0b-b059-85d63de31a9f.htseq.counts.gz	7207f6f35a1b2044035b700eb4e68aa9	248552	released
		999f701a-2bd2-4e9d-94af-08d0f1be769c	dc76cdde-f77f-4604-94c4-0b150b9a56b4.FPKM.txt.gz	80e7f3092027e21e879633c74596aa37	509899	released
		96332d27-a064-4ca5-bf5d-f9c357556c39	d011c9fc-3598-4f0b-b059-85d63de31a9f.FPKM-UQ.txt.gz	9aadc0fd9352dccf65e509ecf186c8a7	503624	released

	Metadata will be outputed to meta.json
