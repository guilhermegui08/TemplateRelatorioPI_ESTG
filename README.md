# TemplateRelatorioPI_ESTG

This repository contains a LaTeX template for dissertations, project reports, or internship reports according to the graphic presentation guidelines of the Escola Superior de Tecnologia e Gestão (ESTG).

## Compilation Setup

1. **latexmkrc Configuration**

   Create a file named `.latexmkrc` in your project directory with the following content:

   ```perl
   # latexmkrc
   # Use pdflatex for compilation
   $pdflatex = 'pdflatex -interaction=nonstopmode -synctex=1 %O %S';
   
   # Use biber for bibliography
   $biber = 'biber %O %S';
   
   # Use makeindex for index
   $makeindex = 'makeindex %O -s %S.ist %S';
   
   # Custom dependencies for glossaries
   add_cus_dep('glo', 'gls', 0, 'makeglossaries');
   add_cus_dep('acn', 'acr', 0, 'makeglossaries');
   
   sub makeglossaries {
       system("makeglossaries $_[0]");
   }
   
   # Ensure correct order of compilation
   $clean_ext .= ' glsdefs';
   
   push @generated_exts, 'glo', 'gls', 'acn', 'acr', 'alg', 'ist';
   
   # Ensure footnotes and other references are resolved
   $pdf_mode = 1;
   $pvc_view_file_via_temporary = 0;
   
   # Number of runs
   $max_repeat = 5;
   
   # Custom clean extensions
   @default_files = qw(aux bbl blg idx ilg ind lof log lot out toc acn acr alg glg glo gls);
   @generated_exts = (@default_files, qw(fls fdb_latexmk synctex.gz));
   
   1;```

