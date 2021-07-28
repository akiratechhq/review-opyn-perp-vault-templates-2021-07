OpynPerpVault

  [x] modifier onlyUnlocked
  [x] modifier onlyLocked
  [x] modifier lockState
      [x] raised issue (#1) about replacing "can" -> "should"
  [x] modifier unlockState
  [x] modifier notEmergency
  [] init
      [] why uses ERC20Upgradeable ? - ask slack
      [] NB: there's no whitelisting of assets
      [] why isn't WETH address hardcoded? - ask slack
      [] _tokenName and _tokenSymbol, being fully user/admin controlled means one
      can create vaults with same symbol/name. What problems would this cause?
      [] why check of duplicated actions? - ask slack (Dani)
  [x] setCap
  [x] totalAsset
  [x] getSharesByDepositAmount
  [x] getWithdrawAmountByShares
  [] deposit
  [] registerDeposit
  [] claimShares
  [] withdraw
  [] registerWithdraw
  [] withdrawFromQueue
  [] closePositions
  [] rollOver
  [] emergencyPause
  [] resumeFromPause
  [] _netAssetsControlled
  [] _totalAssets
  [] _effectiveBalance
  [] iterates
  [] _totalDebt
  [] _deposit
  [] _closeAndWithdraw
  [] _distribute
  [] _withdrawFromQueue
  [] _regularWithdraw
  [] _getSharesByDepositAmount
  [] _getWithdrawAmountByShares
  [] _payRoundFee
  [] _snapshotShareAndAsset
