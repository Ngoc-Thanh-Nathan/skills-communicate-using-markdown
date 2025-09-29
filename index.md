# Voici un titre de taille \<H1> via le markdown
C'est le début de mon utilisation de github

![Image of Duck](https://mystickermania.com/cdn/stickers/memes/duck-with-knife-meme-512x512.png)

``` c
void CLK_Setup(){
    // Configure la pin D2 (PA10) pour la sortie du timer TCC0/WO[2]
  PORT->Group[PORTA].PINCFG[10].bit.PMUXEN = 1;
  PORT->Group[PORTA].PMUX[10 >> 1].reg &= ~(0xF << (4 * (10 & 0x01)));
  PORT->Group[PORTA].PMUX[10 >> 1].reg |= (5 << (4 * (10 & 0x01))); // Fonction E: TCC0/WO[2]

  // Active le timer TCC0
  GCLK->CLKCTRL.reg = GCLK_CLKCTRL_ID(GCLK_CLKCTRL_ID_TCC0_TCC1_Val) |
                      GCLK_CLKCTRL_GEN_GCLK0 | GCLK_CLKCTRL_CLKEN;
  while (GCLK->STATUS.bit.SYNCBUSY);

  TCC0->WAVE.reg = TCC_WAVE_WAVEGEN_NPWM; // Mode PWM
  while (TCC0->SYNCBUSY.bit.WAVE);

  TCC0->PER.reg = 15; // 48MHz/(PER+1) = 3MHz
  while (TCC0->SYNCBUSY.bit.PER);

  TCC0->CC[2].reg = 7; // Rapport cyclique 50% sur canal 2
  while (TCC0->SYNCBUSY.bit.CC2);

  TCC0->CTRLA.bit.ENABLE = 1;
  while (TCC0->SYNCBUSY.bit.ENABLE);
}


```
