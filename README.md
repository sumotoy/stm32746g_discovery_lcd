# stm32746g_discovery_lcd
A more complete BSP driver for STM32F7 discovery retro-compatible

I just get my first ST32 board, the STM32F7 discovery, nice features, nice speed, fully equipped, but a mess to program, spent 2 days just to understand wich IDE to use!
I wonder why ST has this horrible approach with such a worderful hardware, if they change directions for sure the ST micros can kick the ass but actually get a led on/off and get display on have the exact amount of complications and I believe it's impossible for a non-professional user to deal with these board, too bad.<br>
ST provide his drivers, almost everyone use it without touching anithing but digging inside code I discover that most are not written as I expect, sometime the performances are poor, the coding it's obscure and not easy to understand. The result it's that coders community don't contribute to get better drivers!<br>
The ST stuff it's powerful and cost much less than many other MCU's, the company spend a fortune to create boards for non-professionals, many has arduino pin compatibility (most un-usable since most arduino shields are 5V and all the ST stuff it's 3v3) but the software it support related it's a mess so most people buy the board because it's really cheap and fully loaded but after a while they give up and leave in a side to accumulate dust.<br>
If someone of ST is reading this it's time to open eyes and change completely direction, or just forget the enthusiasts market and continue to sell for consumer professionals!<br>
Apart these considerations, I need to do something with my board before put in a side to get dust so I've started digging code and started with the BSP driver for the discovery 480x272 capacitive touch screen LCD.<br>
The TFT it's RK043FN48H-CT672B from Rocktech, again the ST actually doesn't provide any datasheet for it so I have to trust the ST driver! (cmon guys) <br>
The library it's called <b>stm32746g_discovery_lcd</b> and has these functions:<br>

uint8_t  BSP_LCD_Init(void);<br>
uint8_t  BSP_LCD_DeInit(void);<br>
uint32_t BSP_LCD_GetXSize(void);<br>
uint32_t BSP_LCD_GetYSize(void);<br>
void     BSP_LCD_SetXSize(uint32_t imageWidthPixels);<br>
void     BSP_LCD_SetYSize(uint32_t imageHeightPixels);<br>

/* Functions using the LTDC controller */<br>
void     BSP_LCD_LayerDefaultInit(uint16_t LayerIndex, uint32_t FrameBuffer);<br>
void     BSP_LCD_LayerRgb565Init(uint16_t LayerIndex, uint32_t FB_Address);<br>
void     BSP_LCD_SetTransparency(uint32_t LayerIndex, uint8_t Transparency);<br>
void     BSP_LCD_SetLayerAddress(uint32_t LayerIndex, uint32_t Address);<br>
void     BSP_LCD_SetColorKeying(uint32_t LayerIndex, uint32_t RGBValue);<br>
void     BSP_LCD_ResetColorKeying(uint32_t LayerIndex);<br>
void     BSP_LCD_SetLayerWindow(uint16_t LayerIndex, uint16_t Xpos, uint16_t Ypos, uint16_t Width, uint16_t Height);<br>
<br>
void     BSP_LCD_SelectLayer(uint32_t LayerIndex);<br>
void     BSP_LCD_SetLayerVisible(uint32_t LayerIndex, FunctionalState State);<br>
<br>
void     BSP_LCD_SetTextColor(uint32_t Color);<br>
uint32_t BSP_LCD_GetTextColor(void);<br>
void     BSP_LCD_SetBackColor(uint32_t Color);<br>
uint32_t BSP_LCD_GetBackColor(void);<br>
void     BSP_LCD_SetFont(sFONT *fonts);<br>
sFONT    *BSP_LCD_GetFont(void);<br>
<br>
uint32_t BSP_LCD_ReadPixel(uint16_t Xpos, uint16_t Ypos);<br>
void     BSP_LCD_DrawPixel(uint16_t Xpos, uint16_t Ypos, uint32_t pixel);<br>
void     BSP_LCD_Clear(uint32_t Color);<br>
void     BSP_LCD_ClearStringLine(uint32_t Line);<br>
void     BSP_LCD_DisplayStringAtLine(uint16_t Line, uint8_t *ptr);<br>
void     BSP_LCD_DisplayStringAt(uint16_t Xpos, uint16_t Ypos, uint8_t *Text, Text_AlignModeTypdef Mode);<br>
void     BSP_LCD_DisplayChar(uint16_t Xpos, uint16_t Ypos, uint8_t Ascii);<br>
<br>
void     BSP_LCD_DrawHLine(uint16_t Xpos, uint16_t Ypos, uint16_t Length);<br>
void     BSP_LCD_DrawVLine(uint16_t Xpos, uint16_t Ypos, uint16_t Length);<br>
void     BSP_LCD_DrawLine(uint16_t x1, uint16_t y1, uint16_t x2, uint16_t y2);<br>
void     BSP_LCD_DrawRect(uint16_t Xpos, uint16_t Ypos, uint16_t Width, uint16_t Height);<br>
void     BSP_LCD_DrawCircle(uint16_t Xpos, uint16_t Ypos, uint16_t Radius);<br>
void     BSP_LCD_DrawPolygon(pPoint Points, uint16_t PointCount);<br>
void     BSP_LCD_DrawEllipse(int Xpos, int Ypos, int XRadius, int YRadius);<br>
void     BSP_LCD_DrawBitmap(uint32_t Xpos, uint32_t Ypos, uint8_t *pbmp);<br>
<br>
void     BSP_LCD_FillRect(uint16_t Xpos, uint16_t Ypos, uint16_t Width, uint16_t Height);<br>
void     BSP_LCD_FillCircle(uint16_t Xpos, uint16_t Ypos, uint16_t Radius);<br>
void     BSP_LCD_FillPolygon(pPoint Points, uint16_t PointCount);<br>
void     BSP_LCD_FillEllipse(int Xpos, int Ypos, int XRadius, int YRadius);<br>
<br>
void     BSP_LCD_DisplayOff(void);<br>
void     BSP_LCD_DisplayOn(void);<br>

Digging the c++ code shows that ST choosed a basic approach, it just reset screen using it's hardware defaults (was hardly difficult but I get an only-for-your-eyes datasheet to prove that) and don't use code trick to accellerate graphic primitives. Also some primitive function it's missed like triangles or arbitrary poligons.<br>
The STM32F7 has internal 2d accelleration but a better tft driver will help a lot with graphic-intensive applications!<br>


