# Dev Notes

* Excel Addin supports maximum .Net version as .Net Framework 4.8, thus for Excel-native hosted graph editor experience, we should target our entire solution to Netstandard 2.0, including the GUI parts - fortunately SFML is built on top of Netstandard 2.0.