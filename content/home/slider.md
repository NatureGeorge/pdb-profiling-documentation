+++
# Slider widget.
widget = "slider"  # See https://sourcethemes.com/academic/docs/page-builder/
headless = true  # This file represents a page section.
active = true  # Activate this widget? true/false
weight = 15  # Order that this section will appear.

# Slide interval.
# Use `false` to disable animation or enter a time in ms, e.g. `5000` (5s).
interval = 10000

# Slide height (optional).
# E.g. `500px` for 500 pixels or `calc(100vh - 70px)` for full screen.
height = ""

# Slides.
# Duplicate an `[[item]]` block to add more slides.
[[item]]
  title = "Want to perform batch retrieval of metadata from PDBe RESTful API?"
  content = "The **P**rotein **D**ata**B**ank is regarded as one of the most valuable resources in bioinformatics researches but requires huge storage to scan through a large amount of PDB entries. The [RESTful services](https://www.ebi.ac.uk/pdbe/pdbe-rest-api) provided by EBI save users' life by providing different API calls that focus on a different aspect of relevant information like data scheme, experimental details, and so on."
  align = "center"  # Choose `center`, `left`, or `right`.

  # Overlay a color or image (optional).
  #   Deactivate an option by commenting out the line, prefixing it with `#`.
  overlay_color = "#333"  # An HTML color value.
  overlay_img = "api_webinars_promo.png"  # Image path relative to your `static/media/` folder.
  overlay_filter = 0.8  # Darken the image. Value in range 0-1.

  # Call to action button (optional).
  #   Activate the button by specifying a URL and button label below.
  #   Deactivate by commenting out parameters, prefixing lines with `#`.
  cta_label = "Learn more"
  cta_url = "https://pdbeurope.github.io/api-webinars/"
  cta_icon_pack = "fas"
  cta_icon = "book"
  
[[item]]
  title = "What is the representative set of my target proteins?"
  content = "The demand for defining a non-redundant set of protein tertiary structures in Monomeric or Homomeric or Heteromeric state is long-standing. With the required information and the user-defined criteria, the greedy algorithm plus the metric used to measure the degree of similarity between sets can be implemented to achieve this goal."
  align = "center"

  overlay_color = "#333"  # An HTML color value.
  overlay_img = "sele_paper.jpg"  # Image path relative to your `static/media/` folder.
  overlay_filter = 0.8  # Darken the image. Value in range 0-1. 

[[item]]
  title = "Want to study in an interactional level?"
  content = "The molecular details contained in the interaction are essential to the understanding of the biological process. And there exists a rich resource that can be dig in the different Assembly of the PDB entry."
  align = "center"

  overlay_color = "#333"  # An HTML color value.
  overlay_img = "au_bu.png"  # Image path relative to your `static/media/` folder.
  overlay_filter = 0.25  # Darken the image. Value in range 0-1.

[[item]]
  title = "Want to perform bidirectional mapping from or to PDBResidue?"
  content = "There exists a logical correspondence from the trinucleotide codon to the amino acids in the polypeptide chain and then to the residues in the protein tertiary structure. This correspondence is based on the sequential property of nucleic acid sequences and the derived polypeptide chain."
  align = "center"

  overlay_color = "#333"  # An HTML color value.
  overlay_img = "genome2pdb.drawio.svg"  # Image path relative to your `static/media/` folder.
  overlay_filter = 0.75  # Darken the image. Value in range 0-1.

+++