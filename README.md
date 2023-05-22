# min-max-calc-scss
A Sass mixin based on the Min-Max-Value Interpolation for font sizing

Based on: https://github.com/9elements/min-max-calculator

Input:
  1. Minimum font size in px
  2. Maximum font size in px
  3. Minimum viewport size in px
  4. Maximum viewport size in px

Notes:
  1. All values in pixels
  2. Min values must be lesser than max values

	@mixin fontSize_minMax($minValuePx, $maxValuePx, $minViewportPx, $maxViewportPx) {
		$minValueREM: ($minValuePx / 16);
		$maxValueREM: ($maxValuePx / 16);
		$variablePart: ($maxValuePx - $minValuePx) / ($maxViewportPx - $minViewportPx);
		$constant: (($maxValuePx - $maxViewportPx * $variablePart) / 16);

		font-size:clamp(#{$minValueREM}rem, #{$constant}rem + #{100 * $variablePart}vw, #{$maxValueREM}rem);
	}


##  Example Usage
	p {
		@include fontSize_minMax(16, 32, 320, 1400);
		// Output: font-size: clamp(1rem, 0.7037037037rem + 1.4814814815vw, 2rem);
	}
	h1 {
		@include fontSize_minMax(24, 48, 320, 2000);
		// Output: font-size: clamp(1.5rem, 1.2142857143rem + 1.4285714286vw, 3rem);
	}
