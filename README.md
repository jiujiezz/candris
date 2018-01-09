# CANDRIS
A Statistical Method for Predicting Cancer Driver Sites and Cancer-specific Selection Pressures

CANDRIS
=====
	Gu Xun			xgu@iastate.edu
	Zhou Zhan		zhanzhou@zju.edu.cn
	Wu Jingcheng		21619014@zju.edu.cn
	Zhao Wenyi		21719052@zju.edu.cn
	Su Zhixi		zxsu@fudan.edu.cn
	Zou Yangyun		yyzou@fudan.edu.cn
	
	
Description
---
	CANDRIS: Predicting Cancer Driver Sites ; V1.0; 2017.12.15
	
	
Usage
---	
	Options:
		-r input ensembl reference file 
		-t threshold of posterior probability
		-i input mutation file
		-s whether to calculate the value of omega0 and omega1 of driver gene ("T" or "F"). Omega0 is the selection pressure of passenger sites, omega1 is the selection pressure of driver sites.
		-f input file including Cn, Cs value for each gene, if -s is chosen 'True'		
		-o1 output file 1, mutation gene list 
		-o2 output file 2, mutation site list
		-h help
	Sample：
		perl candris.pl -r reference -t threshold -i ICGC(.tsv)/TCGA(.maf)/preprocessed data -s T -f Cn,Cs_value_for_each_gene -o1 gene_with_driver_mutation_sites -o2 driver_mutation_sites 
		perl candris.pl -r reference -t threshold -i ICGC(.tsv)/TCGA(.maf)/preprocessed data -s F  -o1 gene_with_driver_mutation_sites -o2 driver_mutation_sites 
	
	
Analysis steps
---	
	1	Data preparation
		1.1 Choose specific version of Ensembl reference file. #ICGC(75_GRCh37.p13)/TCGA(80_GRCh38.p2)/preprocessed data# The first two are processed and offered beforehand.
		1.2 Collect mutation data from ICGC(.tsv)/TCGA(.maf)/preprocessed data and save it as an mutation file. Its format should be as follows:
			gene_id	trancript_id	DNA_mutation	protein_mutation	mutation_count
			ENSG00000084734 ENST00000264717 1740C>A  F580L  1
			ENSG00000120669 ENST00000379881  389G>A  S130N  1
			ENSG00000011258 ENST00000415868  547A>G  T183A  1
			ENSG00000160716 ENST00000368476  758T>C  I253T  1
			ENSG00000141867 ENST00000263377 3139C>T R1047W  1
		1.3 Prior to determine the threshold of posterior probability.
		1.4 Input file including Cn, Cs value for each gene.
		
	2	CANDRIS input
		2.1 Ensembl reference file  
		2.2 Mutation file 
		2.3 Threshold of posterior probability
		2.4 (OPTIONAL) Input file including Cn, Cs value for each gene
		
	3	Perform CANDRIS
		As shown by usage.
		
	4	Output files in your path 
		You will get two output files: gene_with_driver_mutation_sites and driver_mutation_sites.
      gene_with_driver_mutation_sites:
				Gene_id	Transcript_id	Chr	Gene_name	Max_hit	Count	Protein_length	Distribution	mut_site	f0	mean	variance	m0	m1	eta	LRT_p-value	Q(z)	zc	number_of_predited	CnCs0	CnCs1	CnCs	chisq_p-value	q-value
				ENSG00000254598	ENST00000528848	11	CSNK2A3	3	51	391	3:380;2:8;2:80;2:250;2:283;2:306;2:312;2:324;1:18;1:24;1:31;1:47;1:65;1:95;1:96;1:99;1:122;1:125;1:128;1:134;1:153;1:155;1:166;1:180;1:186;1:187;1:199;1:228;1:233;1:256;1:271;1:277;1:288;1:316;1:328;1:333;1:334;1:338;1:351;1:354;1:382;1:385;	42	0.892583120204604	0.130434782608696	0.164994425863991	0.113635637782939	2.18766112441075	0.00809977742996355	0.067671
				ENSG00000029559	ENST00000226284	4	IBSP	3	55	317	3:163;3:257;2:14;2:57;2:86;2:126;2:264;2:274;1:5;1:19;1:20;1:24;1:41;1:43;1:44;1:80;1:83;1:94;1:102;1:105;1:116;1:143;1:148;1:153;1:154;1:157;1:164;1:178;1:182;1:189;1:196;1:201;1:224;1:234;1:236;1:238;1:245;1:259;1:268;1:281;1:286;1:288;1:295;1:296;1:302;	45	0.858044164037855	0.173501577287066	0.219801940662061	0.153099707581283	2.44291923570251	0.00890981557944981	0.14417
				ENSG00000205726	ENST00000381318	21	ITSN1	3	150	1721	3:830;3:973;2:188;2:678;2:1090;2:1425;2:1513;2:1547;1:9;1:26;1:30;1:36;1:53;1:66;1:84;1:85;1:89;1:91;1:93;1:96;1:106;1:110;1:112;1:138;1:148;1:156;1:168;1:169;1:187;1:236;1:248;1:265;1:283;1:360;1:361;1:382;1:410;1:417;1:421;1:439;1:447;1:451;1:453;1:464;1:466;1:483;1:496;1:528;1:530;1:551;1:561;1:563;1:571;1:575;1:609;1:611;1:625;1:628;1:637;1:643;1:651;1:661;1:672;1:687;1:707;1:727;1:747;1:759;1:783;1:787;1:790;1:802;1:805;1:834;1:838;1:840;1:851;1:856;1:884;1:897;1:903;1:905;1:917;1:933;1:942;1:975;1:978;1:981;1:1009;1:1048;1:1049;1:1052;1:1087;1:1091;1:1126;1:1173;1:1195;1:1206;1:1214;1:1221;1:1224;1:1225;1:1238;1:1282;1:1284;1:1298;1:1302;1:1314;1:1335;1:1346;1:1372;1:1386;1:1419;1:1422;1:1424;1:1460;1:1461;1:1465;1:1468;1:1485;1:1487;1:1493;1:1502;1:1531;1:1532;1:1552;1:1554;1:1566;1:1571;1:1581;1:1595;1:1600;1:1618;1:1620;1:1681;1:1683;1:1684;1:1690;1:1710;1:1720;	140	0.918651946542708	0.0871586287042417	0.0935617474967234	0.0848479590020674	2.85826814143825	0.000833148080773199	0.15743
				ENSG00000127603	ENST00000372915	1	MACF1	3	597	7388	3:3168;3:7286;2:12;2:157;2:801;2:849;2:1574;2:1772;2:1843;2:2112;2:2161;2:2858;2:2882;2:2944;2:3055;2:3101;2:3659;2:3747;2:4291;2:4785;2:4864;2:4925;2:4933;2:4986;2:5119;2:5134;2:5387;2:5888;2:6209;2:6276;2:6915;2:6961;2:7037;2:7081;2:7112;2:7177;2:7277;1:6;1:18;1:24;1:30;1:36;1:45;1:64;1:76;1:81;1:94;1:104;1:115;1:140;1:208;1:213;1:214;1:234;1:239;1:252;1:275;1:287;1:310;1:315;1:344;1:346;1:352;1:359;1:393;1:397;1:401;1:406;1:412;1:418;1:420;1:422;1:424;1:437;1:443;1:454;1:476;1:478;1:479;1:494;1:495;1:526;1:532;1:539;1:587;1:591;1:602;1:607;1:630;1:688;1:703;1:705;1:716;1:722;1:739;1:752;1:794;1:811;1:819;1:833;1:845;1:851;1:856;1:861;1:888;1:894;1:898;1:957;1:993;1:1005;1:1010;1:1028;1:1035;1:1046;1:1051;1:1052;1:1057;1:1059;1:1075;1:1083;1:1086;1:1097;1:1110;1:1123;1:1127;1:1131;1:1132;1:1167;1:1177;1:1187;1:1190;1:1194;1:1195;1:1219;1:1231;1:1243;1:1244;1:1252;1:1255;1:1281;1:1288;1:1301;1:1333;1:1340;1:1343;1:1346;1:1349;1:1354;1:1355;1:1358;1:1367;1:1368;1:1381;1:1393;1:1412;1:1421;1:1430;1:1432;1:1442;1:1470;1:1506;1:1535;1:1553;1:1569;1:1605;1:1615;1:1617;1:1618;1:1622;1:1631;1:1638;1:1644;1:1656;1:1664;1:1685;1:1687;1:1719;1:1740;1:1745;1:1759;1:1780;1:1784;1:1801;1:1812;1:1836;1:1852;1:1854;1:1862;1:1870;1:1871;1:1906;1:1924;1:1938;1:1967;1:1982;1:2022;1:2077;1:2093;1:2099;1:2105;1:2141;1:2148;1:2152;1:2174;1:2184;1:2191;1:2199;1:2200;1:2207;1:2219;1:2222;1:2238;1:2286;1:2293;1:2301;1:2309;1:2324;1:2351;1:2382;1:2387;1:2426;1:2435;1:2465;1:2493;1:2496;1:2538;1:2550;1:2559;1:2561;1:2581;1:2583;1:2607;1:2608;1:2612;1:2626;1:2658;1:2660;1:2686;1:2687;1:2710;1:2711;1:2738;1:2773;1:2782;1:2783;1:2821;1:2827;1:2829;1:2836;1:2856;1:2861;1:2867;1:2872;1:2880;1:2883;1:2898;1:2903;1:2907;1:2915;1:2927;1:2943;1:2957;1:2993;1:3020;1:3022;1:3034;1:3037;1:3076;1:3084;1:3096;1:3099;1:3104;1:3132;1:3202;1:3207;1:3214;1:3220;1:3232;1:3264;1:3276;1:3277;1:3278;1:3285;1:3338;1:3356;1:3365;1:3375;1:3394;1:3457;1:3485;1:3506;1:3507;1:3537;1:3540;1:3545;1:3551;1:3562;1:3588;1:3591;1:3609;1:3649;1:3650;1:3667;1:3669;1:3712;1:3721;1:3731;1:3740;1:3751;1:3773;1:3781;1:3794;1:3802;1:3812;1:3838;1:3842;1:3871;1:3883;1:3895;1:3900;1:3914;1:3930;1:3949;1:3961;1:3963;1:3968;1:3970;1:3972;1:3976;1:4013;1:4019;1:4027;1:4055;1:4057;1:4066;1:4070;1:4080;1:4094;1:4096;1:4099;1:4128;1:4172;1:4173;1:4197;1:4201;1:4230;1:4255;1:4264;1:4287;1:4313;1:4352;1:4356;1:4373;1:4385;1:4398;1:4433;1:4486;1:4552;1:4573;1:4591;1:4599;1:4667;1:4713;1:4717;1:4769;1:4779;1:4781;1:4789;1:4793;1:4799;1:4813;1:4816;1:4832;1:4833;1:4849;1:4855;1:4862;1:4867;1:4895;1:4923;1:4944;1:4958;1:5012;1:5015;1:5064;1:5080;1:5116;1:5130;1:5132;1:5142;1:5155;1:5172;1:5176;1:5183;1:5184;1:5190;1:5224;1:5257;1:5265;1:5275;1:5282;1:5291;1:5320;1:5322;1:5324;1:5330;1:5346;1:5365;1:5369;1:5379;1:5392;1:5402;1:5410;1:5420;1:5434;1:5460;1:5472;1:5473;1:5497;1:5570;1:5572;1:5580;1:5590;1:5667;1:5685;1:5689;1:5743;1:5765;1:5773;1:5791;1:5821;1:5824;1:5835;1:5836;1:5845;1:5862;1:5867;1:5893;1:5908;1:5910;1:5920;1:5925;1:5979;1:5983;1:5999;1:6013;1:6015;1:6025;1:6026;1:6037;1:6040;1:6060;1:6065;1:6066;1:6074;1:6108;1:6109;1:6137;1:6142;1:6147;1:6171;1:6188;1:6191;1:6194;1:6205;1:6250;1:6255;1:6261;1:6262;1:6265;1:6266;1:6267;1:6278;1:6285;1:6291;1:6299;1:6309;1:6342;1:6345;1:6368;1:6379;1:6393;1:6406;1:6411;1:6421;1:6433;1:6448;1:6488;1:6491;1:6521;1:6528;1:6537;1:6542;1:6550;1:6589;1:6632;1:6639;1:6644;1:6651;1:6655;1:6659;1:6663;1:6685;1:6686;1:6688;1:6730;1:6747;1:6757;1:6763;1:6791;1:6810;1:6819;1:6820;1:6834;1:6842;1:6843;1:6860;1:6869;1:6872;1:6875;1:6892;1:6905;1:6908;1:6923;1:6932;1:6939;1:6958;1:6968;1:6988;1:6994;1:7016;1:7042;1:7054;1:7066;1:7068;1:7073;1:7075;1:7080;1:7083;1:7087;1:7096;1:7148;1:7158;1:7161;1:7164;1:7166;1:7181;1:7199;1:7222;1:7244;1:7248;1:7263;1:7272;1:7273;1:7283;1:7327;1:7367;1:7376;	558	0.9244721169464	0.0808067135896048	0.0853876258274009	0.0785323887542949	2.09499227172776	0.00112788003099579	0.10848
      driver_mutation_sites:
				Gene_id	Transcript_id	Chr	Gene_name	Protein_position	z	Q(z)	Protein_mutation
				ENSG00000106278	ENST00000393386	7	PTPRZ1	833	5	0.998756375217605	R833C:4;R833H:1;
				ENSG00000106278	ENST00000393386	7	PTPRZ1	636	4	0.968955612892411	S636L:3;S636T:1;
				ENSG00000106278	ENST00000393386	7	PTPRZ1	205	3	0.548130755870424	R205H:2;R205C:1;
				ENSG00000106278	ENST00000393386	7	PTPRZ1	515	3	0.548130755870424	D515N:3;
				ENSG00000106278	ENST00000393386	7	PTPRZ1	612	3	0.548130755870424	E612K:3;
				ENSG00000105641	ENST00000222248	19	SLC5A5	569	5	0.999903970051843	R569W:5;
				ENSG00000105641	ENST00000222248	19	SLC5A5	438	3	0.896681963701284	P438S:2;P438L:1;		
		The meaning of some parameters in the result:
			Max_hit：the maximum number of mutations at each site of a gene		Count：the total number of mutations in a gene
			Distribution：mutation distribution at all sites of a gene			mut_site：all mutation sites in a gene
			f0：the ratio of non-mutated sites in a gene						mean：the average number of mutations at all sites of a gene
			m0：the average number of mutations on the passenger_site			m1：the average number of mutations on the driver_site
			eta：the number of driver_site at all sites of a gene				LRT_p-value：Likelihood Ratio Test value
			Q(z)：posterior probability											z：The number of mutations in the locus
			zc：cutoff															number_of_predited：the number of driver_site in a gene				
			CnCs：the rate ratio of somatic nonsynonymous to synonymous substitutions (CN/CS) of a protein-encoding gene																															
			CnCs0：	CN/CS ratios for passenger sites of a gene					CnCs1：CN/CS ratios for cancer driver sites of a gene															
			chisq_p-value：Chi-squared Test	value								q-value：the p-value of the FDR correction												




		
		
